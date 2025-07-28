---
abbrlink: ''
categories: []
date: '2025-07-28T11:49:46.584295+08:00'
tags: []
title: Docker 部署的 openWrt 软路由并解决与宿主机通信问题
updated: '2025-07-28T11:49:50.941+08:00'
---
### 1.OpenWrt

1）打开网卡混杂模式

```
ip link set eth0 promisc on
```

2）创建OpenWrt网络(自行替换网段，网关)

```
docker network create -d macvlan --subnet=192.168.10.0/24 --gateway=192.168.10.1 -o parent=eth0 openwrt
```

3）下载镜像包至root

```
wget https://dl.openwrt.ai/releases/targets/meson/meson8b/openwrt-02.01.2024-meson-meson8b-thunder-onecloud-rootfs.tar.gz
```

(这是使用openwrt.ai的固件，如果想用最新版，可以自行替换链接)

4）生成镜像

```
docker import openwrt-02.01.2024-meson-meson8b-thunder-onecloud-rootfs.tar.gz onecloud/openwrt
```

5）安装并启动容器

```
docker run --restart always --name openwrt -d --network openwrt --privileged onecloud/openwrt /sbin/init
```

［此固件默认IP为10.0.0.1 密码root］

6）修改默认IP
①直接通过终端修改

```
#进入容器
docker exec -it openwrt bash
#打开网络配置文件
nano /etc/config/network
#重启网络
/etc/init.d/network restart
```

②修改电脑网段，在浏览器通过默认IP访问后修改


### 2.容器与宿主机的通讯修复


#### 造成原因及解决方法说明

[#](https://www.treesir.pub/post/n1-docker/#%e9%80%a0%e6%88%90%e5%8e%9f%e5%9b%a0%e5%8f%8a%e8%a7%a3%e5%86%b3%e6%96%b9%e6%b3%95%e8%af%b4%e6%98%8e)

> 原因是部署 openWRT 系统时使用到了 `docker` 的 `macvlan` 模式，这个模式通俗一点讲就是在一张物理网卡上虚拟出两个虚拟网卡，具有不同的MAC地址，可以让宿主机和docker同时接入网络并且使用不同的ip，此时 docker 可以直接和同一网络下的其他设备直接通信，相当的方便，但是这种模式有一个问题，宿主机和容器是没办法直接进行网络通信的，如宿主机ping容器的ip，尽管他们属于同一网段，但是也是ping不通的，反过来也是。因为该模式在设计的时候，为了安全禁止了宿主机与容器的直接通信，不过解决的方法其实也很简单——宿主机虽然没办法直接和容器内的 `macvlan` 接口通信，但是只要在宿主机上再建立一个 `macvlan`，然后修改路由，使数据经由该 `macvlan` 传输到容器内的 `macvlan` 即可，`macvlan` 之间是可以互相通信的。


#### 具体步骤记录

[#](https://www.treesir.pub/post/n1-docker/#%e5%85%b7%e4%bd%93%e6%ad%a5%e9%aa%a4%e8%ae%b0%e5%bd%95)

> **以下操作都在小钢炮宿主机上运行**
>
> ### 新增一个mynet的 `macvlan` 接口 (注意不要和原容器的macvlan网卡重名)
>
> [#](https://www.treesir.pub/post/n1-docker/#%e6%96%b0%e5%a2%9e%e4%b8%80%e4%b8%aamynet%e7%9a%84-macvlan-%e6%8e%a5%e5%8f%a3--%e6%b3%a8%e6%84%8f%e4%b8%8d%e8%a6%81%e5%92%8c%e5%8e%9f%e5%ae%b9%e5%99%a8%e7%9a%84macvlan%e7%bd%91%e5%8d%a1%e9%87%8d%e5%90%8d)

```shell
ip link add mynet link eth0 type macvlan mode bridge
```

#### 为该接口分配ip，并启用

[#](https://www.treesir.pub/post/n1-docker/#%e4%b8%ba%e8%af%a5%e6%8e%a5%e5%8f%a3%e5%88%86%e9%85%8dip%e5%b9%b6%e5%90%af%e7%94%a8)

```shell
ip addr add 192.168.1.100 dev mynet
ip link set mynet up
```

#### 添加静态路由使宿主机与openWRT的通信报文使用mynet进行

[#](https://www.treesir.pub/post/n1-docker/#%e6%b7%bb%e5%8a%a0%e9%9d%99%e6%80%81%e8%b7%af%e7%94%b1%e4%bd%bf%e5%ae%bf%e4%b8%bb%e6%9c%ba%e4%b8%8eopenwrt%e7%9a%84%e9%80%9a%e4%bf%a1%e6%8a%a5%e6%96%87%e4%bd%bf%e7%94%a8mynet%e8%bf%9b%e8%a1%8c)

```shell
ip route add 192.168.1.66 dev myne
```


#### 写入开机自启动脚本中

[#](https://www.treesir.pub/post/n1-docker/#%e5%86%99%e5%85%a5%e5%bc%80%e6%9c%ba%e8%87%aa%e5%90%af%e5%8a%a8%e8%84%9a%e6%9c%ac%e4%b8%ad)

```shell
cat >> /etc/rc.local << EOF
ip link add mynet link eth0 type macvlan mode bridge 
ip addr add 192.168.1.100 dev mynet
ip link set mynet up
ip route add 192.168.1.66 dev mynet
EOF
```
#### 确保开机自启脚本添加了 `可执行` 权限

[#](https://www.treesir.pub/post/n1-docker/#%e7%a1%ae%e4%bf%9d%e5%bc%80%e6%9c%ba%e8%87%aa%e5%90%af%e8%84%9a%e6%9c%ac%e6%b7%bb%e5%8a%a0%e4%ba%86-%e5%8f%af%e6%89%a7%e8%a1%8c--%e6%9d%83%e9%99%90)

复制

```shell
chmod a+x /etc/rc.local
```
