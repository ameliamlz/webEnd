工作区（用户操作的地方）->add->暂存区->commit->本地仓库区->push->远程仓库



## 用户信息配置

- git config --global user.name xxx
- git config --global user.email xxx
- 查看配置：git config --list
- 密钥配置：(连接远程仓库，可添加多个) ssh-keygen -t -rsa -C “2459849298@qq.com”



## 本地和远程关联

1、在GitHub上创建一个账户

2、git remote add origin xxx(链接)

3、git push -u origin master(只有第一次需要这样做)



## 基本命令

- 查看本地已存放：git ls-files
- git init \#创建版本库/仓库
- git status
- git add xxx
- git commit -m “....”
- git diff xxx
- git log
- git remote rm origin 移除远程仓库
- git clone 拷贝仓库

\#创建和分支合并

- git branch 查看所有分支
- git branch xxx 创建xxx分支
- git checkout xxx 切换到某分支
- git checkout -b xxx 创建并切换分支
- git merge 分支名 （fast-forward快进模式）
- git branch -d 分支名 #删除分支 （合并完之后）

\#多人协作

- git remote -v 查看远程库的信息
- git push origin master
- git checkout –b dev origin/dev 关联远程分支和本地分支
- git pull 合并产生冲突时，先pull合并再提交，指定链接



## GIT

Merge Request and Pull Request解决冲突:

当你在自己的分支上做了提交，并commit后。

从自己的分支切换到master: git checkout master

在master分支拉取最新分支：git pull

然后再切换到自己的分支执行rebase操作: git checkout feature/ && git rebase master



## 如何将别人项目修改后，提交到自己的GitHub

1. 方法一：修改.git/config这个文件，把url换成自己新建的仓库地址
2. 方法二：利用fork，直接clone & push

当原项目更新后，你fork的项目如何更新？

1. `git clone` 原项目到本地

2. 在 github 上 `fork` 该项目，这时有了自己的仓库地址 url

3. 执行 `git remote add name url`，name 是你的仓库别名，可以随便改但不要跟已有的冲突

4. 最后，通过 `git fetch origin` 来获取原项目的最新代码

5. `git merge -m <msg>`  大功告成！

   

## git merge 和 git rebase 的区别

git merge：自动创建一个新的commit，遇到冲突时，修改后commit即可，这样保留了真实的commit情况(优点)

git rebase: 变基，即找公共祖先，会合并之前的commit历史，遇到冲突时，修改冲突，再git add, 继续变基git rebase --continue

