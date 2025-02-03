---
abbrlink: ''
categories: []
date: '2025-02-03T13:07:48.816166+08:00'
tags: []
title: Github推送
updated: '2025-02-03T13:07:39.875+08:00'
---
步骤如下:

1. 拉取远程仓库的更改:
   ```
   git pull origin main
   ```
   这个命令会从远程仓库 origin 的 main 分支拉取最新的提交，并尝试合并到你的本地 main 分支。
2. 解决冲突 (如果存在):
   如果 git pull 命令提示有冲突，你需要手动解决这些冲突。Git 会在冲突的文件中标记出冲突的部分，你需要编辑这些文件，选择保留哪些更改，然后将文件标记为已解决。
3. 提交合并后的更改:
   ```
   git add .
   git commit -m "Merge remote changes"
   ```
   将解决冲突后的文件添加到暂存区，并提交合并后的更改。
4. 推送你的本地更改:
   ```
   git push origin main
   ```
   现在，你的本地 main 分支和远程仓库的 main 分支同步了，你可以成功推送你的本地更改。
