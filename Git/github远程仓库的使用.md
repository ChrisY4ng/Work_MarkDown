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

## git-版本回退与撤销的相关命令及解释

- $:git reset --hard <commitID>  --> 回退到指定commit（HEAD指向当前版本）
- $:git checkout -- <fileName>  --> 将文件在工作区的修改全部撤销（丢弃工作区的修改），用commit或者暂存区中文件替代
- $:git reset HEAD <fileName>  --> 将暂存区的修改回退到工作区（HEAD表示最新的版本）

## git-删除文件相关命令及解释

- $:git rm <fileName>  --> 从版本库删除文件（还需要git commit来提交）

## git-远程仓库相关命令及解释

- $:git remote add origin git@github.com:chris/gitName.git  --> 添加远程仓库  
- $:git push [-u] <origin> <master>  --> 将本地库的内容推送到远程库，-u用来将本地master和远程master关联起来,origin指定远程库，master指定要推送的指定分支到远程库的关联分支(若要推送dev分支则应改为dev)  
- $:git clone git@github.com:chris/gitName.git  --> 从远程仓库克隆一个本地库  
- $:git pull
- $:git remote [-v]  --> 查看远程库的信息(-v信息更加详细，fetch对应抓取权限，push对应推送权限)
- $:git checkout -b dev origin/dev  --> 创建远程分支到本地
- $:git branch [--set-upstream] dev origin/dev 指定本地分支和远程分支的链接(当远程库中的分支版本高于/提前与本地分支时，需要从新指定链接并git pull)
- $:git pull
- $:git remote rm origin  --> 删除关联的远程库（可进行重新关联，同一个本地库可以关联到两个不同名的远程库） 

## git-分支相关命令及解释

- $:git branch <branchName>  --> 创建名为branchName的分支
- $:git checkout <branchName>  --> 从默认的master主支切换到名为branchName的分支
- $:git checkout -b <branchName>  --> 创建名为branchName的分支，并从master切换到此分支
- $:git branch  --> 用来查看当前拥有的分支情况，‘*’号标明当前所在分支
- $:git merge <branchName>  --> 将指定名字的分支合并到当前分支(若需将新建分支合并到master，需先切换到master),当合并分支发生冲突时需先解决冲突后再提交
- $:git branch -d <branchName>  --> 删除指定分支
- $:git branch -D <branchName>  --> 强行删除指定分支

### git-bug分支

- $:git stash  --> 将当前分支工作区中的文件暂存到储藏区，使工作区显式为空，可以进行其他处理
- $:git stash list  --> 查看刚才分支下的零时存储(需先切换到存储时的分支)
- $:git stash apply --> 将储藏区中的内容恢复到工作区，但储藏区中的文件不删除
- $:git stash drop  --> 用于将储藏区中的文件删除
- $:git stash pop  --> 将储藏区中的文件恢复并删除
- $:git stash apply [stash@{0}]  -->当多次stash后，恢复指定stash

### GIT分支合并模式

1. Fast-forward 合并为“快进模式”，将master纸箱当前分支，影响是速度快但会丢掉相应的分支信息
    - $:git merge --no-ff -m "commit message" <branchName>  --> 禁用Fast-forward模式，在merge时生成一个新的commit
2. Auto-merge 自动合并模式，当自动合并失败时，需要手动合并来解决

## git-标签相关命令及解释

- $:git tag <tagName,eg:v_1.0>  --> 打标签，默认为给最新的commit打标签
- $:git tag <tagName> <commitID>  --> 给指定commit打标签
- $:git tag  --> 查看所有标签
- $:git show <tagName>  --> 查看指定标签的信息
- $:git tag -a <tagName> -m "message" <commitID>  --> 创建带有说明的标签
- $:git tag -s <tagName> -m "message" <commitID>  --> 用私钥签名一个标签（签名使用PGP，需首先安装gpg（GnuPG）或有gpg密钥对，用pgp签名的标签不可伪造）
- $:git tag -d <tagName>  --> 删除指定标签
- $:git push origin <tagName>  --> 将标签推送到远程（标签默认存储在本地，不会被推送到远程，打错的标签在不推送前可以安全删除）
- $:git push origin --tags  --> 一次性推送全部尚未推送的标签
- $:git tag -d <tagName>
- $:git push origin:refs/tag/<tagName>  --> 从远程删除标签，需要先从本地删除，再提交

## git-配置相关命令及解释

- 配置等级 [env]:--system/global/local  --> 系统/全局/当前项目

- $:git config [env] user.name [userName]  --> 设置用户名
- $:git config [env] user.email [userEmail]  --> 设置邮箱
- $:git config [env] color.ui <true>  --> 让git显式颜色

## git-.gitignore来忽略文件

**在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。**

忽略文件原则
1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

- $:git check-ignore -v <fileName>  --> 检查是否忽略了指定文件
- $:git add -f <fileName>  --> 忽略ignore配置，强制添加文件到git

## git-配置命令别名

- $:git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  --> 将git log --color ....别名为 git lg  
*别名存放在.git/config文件中的[alias]下*


## git-信息查看

- $:git status  --> 用于查看git工作区的当前状态
- $:git log [--graph] [--pretty=oneline] [--abbrev-commit]  --> 用于查看git的日志信息
- $:git reflog  --> 查看之前使用的命令
- $:git config -l  --> 列出所有配置
- $:git diff  --> 查看修改内容eg：git diff HEAD -- <fileName>