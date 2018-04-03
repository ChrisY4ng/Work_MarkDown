[TOC]

# GITHUB 远程仓库的使用

## 连接GITHUB

1. 创建SSH Key:ssh-keygen -t rsa -C "email"
2. 登陆GITHUB，打开Account Setting，SSH KEYs页面
3. add SSH Key
4. 测试GitHub连接：ssh -T git@github.com

## GITHUB建库

1. 登陆GITHUB，Create a new repo
2. 关联远程库：git remote add origin git@github.com:GitHubName/repository.git
3. 首次提交本地仓库到远程：git push -u origin master（-u:用来关联本地仓库与远程仓库）
4. 再次提交（简化命令）：git push origin master

5. 克隆远程仓库：git clone git@github.com:GitHubName/repositoryName.git