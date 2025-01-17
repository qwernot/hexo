---
title:  Git超时解决
date: '2024/1/17 18:00:00'
top_img: 'https://t.mwm.moe/fj'
cover: 'https://t.mwm.moe/fj'
comments: 是否开启评论(true or false)
no_word_count: true <!-- 关闭字数统计 -->
reward: true <!-- 当前文章是否开启打赏 -->
copyright: true <!-- 当前文章是否开启版权声明 -->
categories: 实用技巧
tags:
  - git,hexo
abbrlink: 22689

---

在写完一天的代码后，我像往常一样进行了hexo d

原本应该在几秒钟上传成功，但是却异常的慢，，这时突然出现一个错误：

Error: Spawn failed

j然后我进行ssh连接测试提示： “ssh:connect to host github.com port 22: Connection timed out”

再多尝试几次，依然是这样。

后来又尝试直接再文件夹里用git命令行提交：
![在这里插入图片描述](https://s2.loli.net/2024/01/17/rpY4KRhyf8zMOCm.png)
可惜结果依然是失败。。。

又尝试重启电脑，结果毫无乱用。

最后通过查阅各种资料，得知原因可能是由于电脑的防火墙或者其他网络原因导致ssh连接方式 端口22被封锁。

### 解决

最终发现两个**解决方案**：

方法一：抛弃ssh连接方式，使用http连接。（我没有用）（似乎没啥用）

操作方法：

1.输入命令：

```
git config --local -e
```

2.将配置文件的url = git@github.com:username/repo.git一行改为：url = https://github.com/username/repo.git
![在这里插入图片描述](https://s2.loli.net/2024/01/17/GkyrCu9IV7Aqi1U.png)

**方法二**：如果22号端口不行，那就换一个端口（我用的，有用）

操作方法：

1.进入~/.ssh下

```yaml
cd ~/.ssh
```

2.创建一个config文件(这里我用的vim编辑器)

```yaml
vim config
```

3.编辑文件内容：

```yaml
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443

Host gitlab.com
Hostname altssh.gitlab.com
User git
Port 443
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
12345678910111213
```

4.保存退出

5.检查是否成功

```yaml
ssh -T git@github.com
```

额，这里要根据它的提示操作，有个地方要输入yes

大功告成，这时候再试试git push，已经可以提交了！

## 报错1

```shell
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (/usr/local/src/hexo/cairbin/node_modules/hexo-util/lib/spawn.js:51:21)
      at ChildProcess.emit (events.js:376:20)
      at Process.ChildProcess._handle.onexit (internal/child_process.js:277:12) {
    code: 128
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
```

### 解决方案

- 进行以下处理

```shell
##进入博客根目录(以我的为例)
cd /usr/local/src/hexo/cairbin/

##删除git提交文件夹
rm -rf .deploy_git/

git config --global core.autocrlf false
```

- 最后重新生成提交

```shell
hexo clean && hexo g && hexo d
```

在提交的过程可能又出现以下报错

## 报错2

```shell
! [remote rejected] master -> master (push declined due to email privacy restrictions)
```

### 解决方案

- 这是因为你的github设置出了问题
- 浏览器进入github.com
- 登陆github -> "+" ->settings
- 取消邮箱选项

- 重新提交

```shell
hexo clean && hexo g && hexo d
```

## 大功告成

如果不报错，重新访问页面，就发现已经提交成功了
