# 				Git 命令学习

### 创建新版本库的方式：

| 命令                  | 功能                   |
| --------------------- | ---------------------- |
| git clone   +仓库地址 | 从远处服务器，复制项目 |
| git init              | 初始化新仓库地址       |

### 修改和提交：

| 命令                          | 功能                               |
| ----------------------------- | ---------------------------------- |
| git status                    | 查看状态                           |
| git add a.txt b.txt           | 提交 a.txt,b.txt到本地库           |
| git add .                     | 提交本地修改或者新建的文件到本地库 |
| git mv                        | 文件改名                           |
| git commit -m"提交到git 远程" | 提交文件到本地文件                 |
| git push origin master        | 提交文件到远程仓库                 |

### 分支操作：

| 命令               | 功能                  |
| ------------------ | --------------------- |
| git branch         | 查看分支              |
| git branch test    | 创建分支（test 分支） |
| git branch -d test | 删除分支              |
| git checkout dev   | 切换分支（dev 分支）  |

### 合并与衍行：

| 命令           | 功能                                                         |
| -------------- | ------------------------------------------------------------ |
| git merge dev  | 切换到master 主分支，执行命令，合并dev 分支的数据,然后在git push origin master 合并到master 分支上 |
| git merge test | 合并test 分支上的内容到当前登录的分支                        |

### 远程操作：

| 命令                                                         | 功能                             |
| ------------------------------------------------------------ | -------------------------------- |
| git remote -v                                                | 查看远程仓库信息                 |
| git remote add  git@github.com:huasxiaopeng/lktbz-git-demo.git | 添加远程仓库版本                 |
| git fetch origin                                             | 从远程仓库获取代码               |
| git pull origin master                                       | 从master 分支下载并合并代码      |
| git push origin master                                       | 上传代码到远程master分支         |
| git push origin --delete [branchname]                        | 删除远程分支                     |
| git remote rm origin                                         | 移除本地仓库与远程仓库之间的链接 |
|                                                              |                                  |
|                                                              |                                  |

### 日志与版本切换

```properties
 #查看提交日志
 git log
commit 8fc4a539a44085da4d10040c53a8a705c6291308 (HEAD -> master)
Author: lktbz <617387614@qq.com>
Date:   Mon Jul 12 09:02:58 2021 +0800

    新增

commit 173cf1c3487f787bf9b559ae741997b4ad375568
Author: lktbz <617387614@qq.com>
Date:   Mon Jul 12 09:01:21 2021 +0800

    啦啦啦

commit df4c632614cee6fef9d42c1b46f9d5c75c54a808
Author: huasxiaopeng <617387614@qq.com>
Date:   Sat Jan 9 23:42:00 2021 +0800

    dev 分支提交

commit f97d43f3eb8f65437e303be45ff438f9a1c0edda
Author: huasxiaopeng <617387614@qq.com>
Date:   Sat Jan 9 23:22:11 2021 +0800

    提交到git 远程


进行版本切换
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (master)
#执行版本切换命令
git reset -hard 432ae255de81f0e2690e93ffc4c22400ad6f688c
```

#### 版本的回退

> git reset -hard HEAD^
>
> 回退到上上个版本
>
> git reset -hard HEAD^^
>
> 或者通过文件名称进行回退
>
> git reset HEAD  xxx/xxx.java 文件方式
>
> **文中通过此方式进行**
>
> git reset HEAD test.txt

#### git add 后想撤销

```properties
#指定文件回退
git rset HEAD xxx/xxx.java
#文中回退test.txt文件
git reset HEAD test.txt
##不指定文件
git reset HEAD^
##回退多个
git reset HEAD^^

```

#### 查看git log

```properties
##git log 可以查看命令记录
$ git log
commit c7c932f69e02fa092dbff47134d16add10d906d2 (HEAD -> master)
Author: lktbz <617387614@qq.com>
Date:   Tue Jul 27 15:05:02 2021 +0800

    git commit 撤消

commit e762bb1e02c27ca6b3004f3355c8fa3977874652 (origin/master, origin/HEAD)
Author: lktbz <617387614@qq.com>
Date:   Sat Jul 17 15:01:19 2021 +0800

    没办法阿里

commit 1664d6931b753be58ae16bcc9a8cf4d640a19238
Author: lktbz <617387614@qq.com>
Date:   Sat Jul 17 14:56:16 2021 +0800

    提交，估计会后悔
```

可以根据需要指定回退

git reset --soft 1664d6931b753be58ae16bcc9a8cf4d640a19238

能不用 --hard 就不用，因为会删除新修改的代码

#### git commit 之后撤销

```properties
#撤销操作，不删除原来新增的代码
$ git  reset --soft HEAD^
#查看
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt

```

```properties
#慎用git reset --hard HEAD^操作，因为会删除修改的代码
#回退很久之前代码，git log 因为时间久被覆盖了，
#所以需要使用reflog 
$ git reflog
e762bb1 (HEAD -> master, origin/master, origin/HEAD) HEAD@{0}: reset: moving to HEAD^
c7c932f HEAD@{1}: commit: git commit 撤消
e762bb1 (HEAD -> master, origin/master, origin/HEAD) HEAD@{2}: reset: moving to head
e762bb1 (HEAD -> master, origin/master, origin/HEAD) HEAD@{3}: clone: from github.com:huasxiaopeng/git-demo.git
```

#### git push 后撤销

```properties
git log查看提交的commmid


$ git log
commit 8622aca4a579bbb65c7255ae797622b4c33187a7 (HEAD -> master, origin/master, origin/HEAD)
Author: xxxcxy <yy_z3em@163.com>
Date:   Wed Apr 15 13:51:08 2020 +0800

    update.sh

commit bc07480025bca168e2136064d795f2bb56eab999
Author: xxxcxy <yy_z3em@163.com>
Date:   Fri Apr 10 14:09:47 2020 +0800

    add

commit 8bd321cd239abc9ebaf70810c7a094b9dec9dc63
Author: xxxcxy <yy_z3em@163.com>
Date:   Thu Apr 9 11:40:27 2020 +0800

    add

commit a0cd8a40263cd012c1ef2a80ef09ed31d9c37f42
Author: xxxcxy <yy_z3em@163.com>
Date:   Thu Apr 9 11:39:26 2020 +0800


#执行撤销操作
 git reset --soft bc07480025bca168e2136064d795f2bb56eab999
 #再次查看
  git log 
  发现没有了。撤销成功
```



### 分支管理实操

###### 分支创建以及切换分支

```properties
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (master)
#创建 dev_lk 分支
$ git checkout -b dev_lk
Switched to a new branch 'dev_lk'

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_lk)
#创建 dev_wang 分支
$ git checkout -b dev_wang
Switched to a new branch 'dev_wang'

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_wang)
#创建 dev_xiao 分支
$ git checkout -b dev_xiao
#查看所有的分支
$ git branch
  dev_lk
  dev_wang
* dev_xiao
  master

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_xiao)
#切换分支
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (master)
#切换分支
$ git checkout dev_lk
Switched to branch 'dev_lk'

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_wang)
#分支的删除
$ git branch -d dev_lk

Deleted branch dev_lk (was 165e66f).
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_wang)
#查看所有的分支
$ git branch
* dev_wang
  dev_xiao
  master
  #强制删除
$ git branch -D dev_lk
```

###### 合并分支以及冲突解决办法

1:xiao同学在自己的分支开发完成并提交到远程，master分支怎么去 合并数据呢？

```properties
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_xiao)
#添加提交的文件
$ git add .

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_xiao)
#在自己的分支提交
$ git commit -m"xiao"
[dev_xiao 1fa53e3] xiao
 1 file changed, 2 insertions(+), 1 deletion(-)

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_xiao)
#上级领导切换分支
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (master)
#合并操作
$ git merge dev_xiao
Updating 165e66f..1fa53e3
Fast-forward
 today.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
#查看主节点是否存在刚刚提交的文件 
$ git log
commit 1fa53e30b63ab6016f56a91c8e65cefcaec8b4cd (HEAD -> master, dev_xiao)
Author: lktbz <617387614@qq.com>
Date:   Mon Jul 12 10:33:35 2021 +0800

    xiao

commit 165e66f9fabfe1b4008c1e3df40399d8b1f5cb84 (dev_wang)
Author: lktbz <617387614@qq.com>
Date:   Mon Jul 12 09:25:32 2021 +0800

    第四次修改

#如果小xiao的工作任务完成的话，(可以)直接删除
git branch -d dev_xiao
```

######  冲突解决办法：

```properties
#小里操作
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_wang)
$ git add .

lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (dev_wang)
$ git commit -m"小王提价"
[dev_wang 60fda8a] 小王提价
 1 file changed, 2 insertions(+), 1 deletion(-)

#master 分支操作
#合并wang分支
git merge dev_wang
#查看状态
git status

#小xiao操作
git add .
git commit-m"xiao提交"

#master 分支操作
#合并xiao分支
git merge dev_xiao
#因为不确定xiao是否提前拉了远程文件
可能会起冲突
<<<<<<< HEAD
这是xiao提交的内容
=======
xiao wang
>>>>>>> dev_wang
手动去除冲突代码
然后
git add .
git commit -m"master 手动处理"
```

###### test/dev 拉取msater更新过的数据方式

```properties
#dev 拉取master 代码
# 1:切换dev 分支 git checkout dev
# 2:合并master代码 git merge master
#3:现在代码只在本地，dev 分支暂时还是旧代码 （如果没有去合并，自己就去合并）
#4： git add 添加合并后的新代码
# git commit-m "提交新合并的代码"
# git push origin dev
#以上步骤则算全部更新本地代码成功
```









### 打标签和忽略文件

查看日志时commitid 太长不容易记住，现在可以通过打标签的方式

```properties
#打标签
git tag v1pre commitid
#打标签并且起别名
lktbz@DESKTOP-B7K679L MINGW64 /d/javamid/git/lktbz-git-demo (master)
$ git tag tutu 91a751b0d5564ee7c1bc9d803d6acc2268317eb9 -m"冲突"

#查看log后的
git log
    冲突实例文件
commit 91a751b0d5564ee7c1bc9d803d6acc2268317eb9 (tag: tutu, origin/master, origin/HEAD)
Author: lktbz <617387614@qq.com>
Date:   Mon Jul 12 10:52:07 2021 +0800
#标签的删除
git tag -d v1pre
```

```properties
#文件的忽略
需要在git下面创建一个.gitignore 
现在直接用idea 忽略文件就好了
```

### 本地与远程仓库

```properties
#本地仓库与远程仓库建立联系
git remonte add  仓库地址

```

# 实际工作流程

#### 前提条件

> 必须存在项目
>
> 怎么去查看git 日志，查看更新的相关代码，防止冲突
>
> 着手写代码时先更新相关代码

#### 代码提交阶段

>提交之前先进行本地更新，查看是否会有代码冲突
>
>检查无误更新本地git 并提交相关分支。

#### 从其他分支合并代码

> 如何从主分支、分分支合并相应代码到本地git仓库

#### git 权限管控这块怎么处理？
