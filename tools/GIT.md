## GIT基本命令

- git log：查看日志，按q退出
- git commit --amend：在没push之前仍可以更改提交的信息，进入编辑模型，ESC退出编辑，wq!保存退出



## GIT提交分支

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

