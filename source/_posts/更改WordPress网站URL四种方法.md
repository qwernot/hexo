---
abbrlink: ''
categories: []
date: '2025-02-02T13:06:10.371334+08:00'
tags: []
title: 更改WordPress网站URL四种方法
updated: '2025-04-03T09:07:39.004+08:00'
---
[WordPress](https://www.wordpress.la/)地址和站点地址是非常重要的字段，因为它们是引用网站到互联网上的地址，以及网站文件的位置。本文将分享四种不同的方法，来轻松更改WordPress网站URL。首先我们来了解下为什么要更改WordPress网站URL?

很多情况下需要更改WordPress URL的原因。例如：

1、将WordPress从本地服务器移动到正式站点时，需要更新站点URL 。

2、如果已将WordPress网站移至新域名，则需要更改网站URL以反映所做的更改。

3、如果要将WordPress移至其他目录，例如从WordPress url中删除/ wordpress /。

4、当将WordPress从HTTP转移到HTTPS时，需要更改它。

除此之外，如果您在WordPress中看到太多重定向错误或在对另一个WordPress错误进行故障排除时，可能需要更改WordPress地址设置。

WordPress地址与站点地址

更改WordPress网站URL时，需要更新两个单独的设置：WordPress地址和站点地址。对于很多初学者可能会造成混淆，因为他们不知道这两者之间的区别。

WordPress地址(URL)：是WordPress文件和文件夹存储的地址，包括管理页面，媒体文件，插件，主题等。

站点地址(URL)：是网站的面向公众的部分。这是访问者将输入的网址，以访问网站，也是我们放在名片上的链接。

对于大多数用户，WordPress地址和站点地址URL都是完全相同的。

但是，在某些情况下，大型公司可能将其WordPress网站托管在其他服务器上，因为它们的公司网站还有许多其他应用程序，并且他们想隔离每个应用程序的托管位置。

但是对于大多数用户而言，这两个WordPress URL需要保持不变。

**一、从仪表盘更改WordPress网站URL**

此方法是最简单的。如果可以正常访问WordPress仪表盘，那么我们建议使用此方法。

登录到WordPress仪表盘，转到 设置 » 常规 页面。在“ WordPress地址”和“站点地址”选项下更改WordPress网站URL。

![更改WordPress网站URL](https://www.wordpress.la/wp-content/uploads/2019/11/wordpressurl.png)

WordPress地址和站点地址通常是相同的。

**二、使用functions.php文件更改WordPress网站URL**

建议无法访问其WordPress网站管理区域的用户使用此方法。

使用FTP客户端连接到WordPress网站，然后转到/ wp-content / themes / your-theme-folder

找到functions.php文件，并使用纯文本编辑器(如Notepad或TextEdit)对其进行编辑。在底部添加以下代码：

update\_option( ‘siteurl’, ‘https://www.liwei8090.com’ );

update\_option( ‘home’, ‘https://www.liwei8090.com’ );

保存更改，然后使用FTP将文件上传回服务器。访问网站，看一切是否恢复正常。此方法的优点是它更新数据库中的站点URL。每次加载功能文件时，WordPress都会更新站点URL的数据库选项。一旦一切恢复正常，别忘了从WordPress函数文件中删除这两行代码。

**三、使用wp-config.php文件更改WordPress网站URL**

仅当不确定要编辑哪个WordPress主题或找不到functions.php文件时，才建议使用此方法。

对于这种方法，将站点URL添加到名为wp-config.php的WordPress配置文件中。此文件位于网站的根文件夹中，并且包含重要的WordPress设置。

只需使用FTP客户端连接到网站，然后编辑wp-config文件。需要在以下代码行的上方添加以下代码：‘That’s all, stop editing! Happy publishing’。

define( ‘WP\_HOME’, ‘https://www.liwei8090.com’ );

define( ‘WP\_SITEURL’, ‘https://www.liwei8090.com’ );

保存所做的更改并将其上传回服务器。之后，访问网站以确保一切正常。

**四、使用phpMyAdmin更改数据库中的WordPress网站URL**

更新WordPress网站网址的另一种方法是直接在WordPress数据库中更改。

首先，您需要进行WordPress数据库备份。此步骤非常重要，可以在发生任何问题时帮助撤消数据库更改。

之后，登录phpMyAdmin后台，在phpMyAdmin界面中，单击左栏中的WordPress数据库。该应用程序现在将在WordPress数据库中显示表格。

在PhpMyAdmin选项表中，找到option\_name为siteurl和home的行。

单击左侧的铅笔图标以编辑每一行，并将option\_value字段更改为新的站点URL。之后，单击右下角的微小Go按钮保存数据库更改。

访问网站以查看一切是否正常。
