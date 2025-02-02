---
abbrlink: ''
categories: []
date: '2025-02-02T13:09:57.326565+08:00'
tags: []
title: （Armbian）空间不足解决办法-docker目录转移
updated: '2025-02-02T13:10:10.437+08:00'
---
设置u盘自动挂载

1.插入u盘

```shell
# 查看u盘路径/大小/type
fdisk -l
# 如/dev/sda4
```

2. 格式化u盘为exc4，保持默认，等待完成

```shell
# 举例
mkfs.ext4 /dev/sda4
```

3.创建挂载目录

```shell
# 举例
mkdir /mnt/upan
```

4. 查看u盘UUID

```shell
# 举例
blkid /dev/sda4
```

5. 修改配置文件，在/etc/fstab后追加

```shell
# 例子，uuid和路径改成自己的
UUID=a63dfbda-29c8-478f-a88e-55796514c961   /mnt/upan/   ext4    defaults    0 0
```

6. 挂载目录修改权限

```shell
chmod -R 777 /mnt/upan/
```

7. 重启

```shell
reboot -n
```

8. 检查

挂载目录下存在lost+found目录即为成功

Docker 修改默认存储路径

1. 在刚刚的挂载目录下创建docker目录

```shell
mkdir /mnt/upan/docker
```

2. 记录原储存路径

```shell
docker info|grep "Docker Root Dir:"
#  Docker Root Dir: /var/lib/docker
```

3. 修改docker的systemd的 docker.service的配置文件

```shell
#查找docker.service的配置文件
systemctl disable docker
systemctl enable docker
#显示结果
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
#编辑文件
nano /lib/systemd/system/docker.service
#如何修改(举例)：
#ExecStart=最后追加--graph=/mnt/upan/docker
```

4. docker服务重启

```shell
systemctl disable docker
systemctl enable docker
systemctl daemon-reload
systemctl restart docker
```

5. 复制原本的文件到docker新目录,要等一会

```shell
# 下面是例子，按2步结果修改cd路径
cd /var/lib/docker
cp ./* /mnt/upan/docker/ -rf
```

6. 重启并检查是否成功

```shell
systemctl restart docker
docker ps
```

7. 没问题的话删除原目录下文件

```shell
rm -rf /var/lib/docker/*
```

最后看看多出来的空间

```shell
df -hT
```
