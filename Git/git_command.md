[TOC]

# GIT Command

- git init
- git add
- git commit
- git commit -m "message"
- git status
- git diff
- git log
- git log --pretty=oneline
- git reset --hard HEAD^[,commit id]  回退版本或者撤销暂存区的修改
- git reflog 查看命令历史
- git diff HEAD --fileName  查看工作区中文件与版本库中文件的差异
- git checkout --fileName 丢弃工作区修改，回退上一个版本
- git rm fileName 从版本库中删除指定文件 之后还需git commit -m ""