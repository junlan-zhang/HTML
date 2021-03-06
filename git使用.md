[TOC]

[git的奇淫技巧](<https://github.com/521xueweihan/git-tips>)

## ssh密钥

```
查看ssh是否安装
$ ssh -v
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
           [-D [bind_address:]port] [-E log_file] [-e escape_char]
           [-F configfile] [-I pkcs11] [-i identity_file]
           [-J [user@]host[:port]] [-L address] [-l login_name] [-m mac_spec]
           [-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address]
           [-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]]
           [user@]hostname [command]

已安装，遂生成.ssh文件
$ ssh-keygen
Your identification has been saved in /Users/zhangjunlan/.ssh/id_rsa.
Your public key has been saved in /Users/zhangjunlan/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Rh+LgmAqx7jDnKyjaYNFjN6EYiWzw7/C7Kyzp5Li5Wo zhangjunlan@MacbookPro

显示当前目录下所有文件和文件夹，包括隐藏的.和..等的详细信息
$ ls -al
total 24
drwx------   6 zhangjunlan  staff   192  4 10 17:07 .
drwxr-xr-x+ 57 zhangjunlan  staff  1824  4 10 11:17 ..
-rw-------   1 zhangjunlan  staff  1675  4 10 17:07 id_rsa
-rw-r--r--   1 zhangjunlan  staff   404  4 10 17:07 id_rsa.pub
drwxr-xr-x   2 zhangjunlan  staff    64  4 10 16:36 key_backup
-rw-r--r--   1 zhangjunlan  staff  1059  3  8 22:01 known_hosts

打开公钥
$ cat id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDRXBM0jD7DMdq9NgQAq/b6h6kBF+GdUWOw4fG2U4EDz9CZbt4Xcr7ByKCIxtGbcJKH3pr0j5bdGoyaePdEc1peWkrBpjA3jpb+uzjkrsdMoyOrLbYPZI/mOOTEcS9S2gyPdLvy61Unx+oHw8DgjzweZwmFt8pm2dshAcFB1b8l2+C7OskEMZZ+rLAyYO3amXhIS5c/x8RoBRiWSmCTTfriNReRftW3eXIIZL7RovSwwaj8pluzTx7QTW3DT39Gs2eLJYiYrtEbfLV+HtY5r/ZmSB1oskJpY4FsZSXFHXeNo5hQLIvlivh7b62HScA3VLQVWME9Hgzb9kGNLkhL5nGz zhangjunlan@MacbookPro
```

`ls`显示不隐藏的文件和文件夹

`ls -a`显示当前目录下的**所有**文件和文件夹包括隐藏的.和..等

`ls -l`显示不隐藏的文件和文件夹的**详细信息**

`ls -al`显示当前目录下**所有**文件和文件夹，包括隐藏的.和..等的**详细信息**



```
桌面上新建ss文件夹
$ cd ss
$ git clone git@codehub.devcloud.huaweicloud.com:ldrcglxtjxsl00001/ss_calendar.git
Cloning into 'ss_calendar'...

显示当前目录下所有文件和文件夹，包括隐藏的.和..等的详细信息
$ ls -al
total 0
drwxr-xr-x   3 zhangjunlan  staff    96  4 10 17:57 .
drwx------+ 97 zhangjunlan  staff  3104  4 10 17:46 ..
drwxr-xr-x  17 zhangjunlan  staff   544  4 10 17:57 ss_calendar

$ cd ss_calendar
$ git status

创建并切换到本地分支zjl（HEAD指针指向了zjl分支）
$ git checkout -b zjl

查看关联的远程仓库
$ git remote
origin

添加当前目录的所有文件到暂存区
$ git add -A/git add .

提交文件到仓库区
$ git commit -m "update"

$ git branch
  dev
* zjl

切换到dev分支
$ git checkout dev

将zjl合并到dev分支
$ git merge zjl

上传文件到远程仓库
git push [远程主机名] [本地分支名]
$ git push origin dev
push成功

fetch下载远程仓库所有变动
(将远程仓库的dev分支克隆下来，在本地建立为temp分支)
$ git fetch origin dev:temp

将temp分支和本地dev分支合并
$ git merge temp

在编辑器里注释修改信息

$ git push origin dev
```

`rm -r ss_calendar/`可以删除仓库

`cd ..`返回上一级目录

`cd ~`进入用户主目录

`cd /`进入根目录

`git checkout dev`切换到dev分支

https://blog.csdn.net/qq_36113598/article/details/78906882

git fetch git pull教程

https://blog.csdn.net/qq_38998213/article/details/81638810

概念解释



## 廖雪峰教程

### 创建版本库

1. 创建一个空目录

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/zhangjunlan/learngit
```

2. 把目录变成git可以管理的仓库：`git init`

```
$ git init
Initialized empty Git repository in /Users/zhangjunlan/learngit/.git/
```

当前目录下还多了一个`.git`的目录，这是Git用来跟踪管理版本库的，不要轻易修改里面的文件，改乱了会破坏Git仓库。这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

```
$ ls -ah
.		..		.git		readme.txt
```

3. 两步将文件添加到版本库

```
# 首先创建文件后放入learngit目录下

# 将文件添加到暂存区
$ git add readme.txt

# 将文件提交到仓库，引号内是提交的说明。
$ git commit -m "wrote a readme file"
```

git add可多次使用，添加多个文件，再用commit添加到仓库。

4. 管理文件版本

修改readme.txt后运行`git status`查看仓库当前状态：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

查看具体修改内容：`git diff`

```
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index d8036c1..5fbfb0d 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distribute version control system.
 Git is free software.
\ No newline at end of file
```

两步提交修改

```
$ git add readme.txt

# commit之前检查仓库状态
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   readme.txt

$ git commit -m "add distributed"
[master 4200e78] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
 
# 查看状态：当前没有需要提交的修改，并且工作目录是干净的
$ git status
On branch master
nothing to commit, working tree clean
```

### 时光机穿梭

#### 版本回退

查看版本历史记录(最近到最远的提交)：`git log`，简化信息可加上`--pretty=oneline`参数

```
$ git log --pretty=oneline
1fd4e7e004123e82b82e71c60c4c6e47e17cdc0f (HEAD -> master) append GPL
b0d7249abe9ced0ade780544dede6900f0821f86 add distributed
b4cca8877c3ab24a70dcda13a74f934be25f4a2f wrote a readme file
```

`HEAD`指向的版本就是当前版本，上一个版本是`HEAD^`,上上一个版本是`HEAD^^`,往上100个版本写成`HEAD-100`。`1fd4e7e004123e82b82e71c60c4c6e47e17cdc0f `是`commit id`(版本号)。

使用`git reset`命令把当前版本`append GPL`回退到`add distributed`

```
$ git reset --hard HEAD^

查看readme.txt版本，果然被还原了。
$ cat readme.txt

此刻查看版本库已经看不到append GPL的版本了，如果命令行没有被关掉，就可以通过commit id回到未来的某个版本。版本号只需写前几位即可，git会自动去找。
$ git reset --hard 1fd4e
如果关掉电脑之后找不到commit id，就通过git reflog查找。
$ git reflog
```

**区别：**

`git log`查看所有提交过的版本信息(commit)，不能查看已经删除的commit记录。

`git reflog`查看本地仓库创建之日起，本地所有与项目更改有关的操作。所有分支的所有操作记录(包括clone，commit和reset操作，已经被删除的commit记录)

#### 工作区和暂存区



![bg2015120901](assets/bg2015120901.png)

1. workspace: 工作区(你在电脑里可以看到的目录learngit)

2. `.git`：版本库(隐藏目录)，包括：

   index/stage：暂存区

   git自动创建的第一个分支`master`以及指向master的一个指针`HEAD`

3. repository: 仓库区(本地仓库)

4. remote: 远程仓库

#### 管理修改https://www.liaoxuefeng.com/wiki/896043488029600/897884457270432

#### 撤销修改

#### 删除文件

### 远程仓库

#### 添加远程仓库

#### 从远程库克隆

### 分支管理

#### 创建与合并分支

#### 解决冲突

#### 分支管理策略

#### Bug分支

#### Feature分支

#### 多人协作

#### Rebase

### 标签管理

#### 创建标签

#### 操作标签

### 使用Github

### 使用码云

### 自定义Git

#### 忽略特殊文件

#### 配置别名

#### 搭建Git服务器






## Git手册

### 新建代码库

```
当前目录新建一个git代码库
$ git init

新建目录，将其初始化为git代码库
$ git init [project-name]

下载一个项目和它的整个代码历史
$ git clone [url]
```

### 配置

git的配置文件是.gitconfig，可以在用户主目录下(全局配置)，也可以在项目目录下(项目配置)。

```
显示当前git配置
$ git config --list

编辑git配置文件
$ git config -e[--global]

设置提交代码时的用户信息
$ git config[--global] user.name "[name]"
$ git config[--global] user.email "[email address]"
```

### 增加删除文件

```
添加文件到暂存区
$ git add [file1] [file2]...

添加指定目录到暂存区，包括子目录
$ git add [dir]

添加当前目录的所有文件到暂存区
$ git add .

添加每个变化之前，都会要求确认
对于同一个文件的多处变化，可以实现分次提交
$ git add -p

删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2]
```

### 代码提交

```
提交暂存区到仓库区
$ git commit -m [message]

提交暂存区的指定文件到仓库区
$ git commit [file1] [file2]... -m [message]

提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

提交时显示所有diff信息
$ git commit -v
```

### 分支

```
列出本地所有分支
$ git branch

列出所有远程分支
$ git branch -r

列出所有远程分支和本地分支
$ git branch -a

新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

新建一个分支，并且切换到该分支
$ git checkout -b [branch]

切换到指定分支，并更新工作区
$ git checkout [branch-name]

切换到上一个分支
$ git checkout -

合并指定分支到当前分支
$ git merge [branch]

删除分支
$ git push origin --delete [branch-name]

删除远程分支
$ git branch -dr [remote-branch]
```

### 查看信息

```
显示有变更的文件
$ git status

显示当前分支的版本历史
$ git log

显示commit历史，以及每次commit发生变更的文件
$ git log --stat
```

### 远程同步

```
更新远程仓储
$ git remote update

下载远程仓库的所有变动
$ git fetch [remote]

显示所有远程仓库
$ git remote -v

显示某个远程仓库的信息
$ git remote show [remote]

增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

上传本地指定分支到远程仓库
$ git push [remote] [branch]

强行推送（即使有冲突）当前分支到远程仓库
$ git push [remote] --force

推送所有分支到仓库
$ git push [remote] --all
```

### 撤销

```
恢复暂存区的指定文件到工作区
$ git checkout [file]

恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

恢复暂存区的所有文件到工作区
$ git checkout .
```



### 错误提交到git远端master如何回滚

1. copy一份本地项目
2. 进入项目根目录，切换到master分支

```
git branch
git checkout master
```

3. 找到github项目所在的master分支，确定需要回退的版本id号

```
git reset --hard [需要回退的版本id号]
```

4. 提示版本落后于分支，此时执行强制提交命令

```
git push -f origin master
```

如果报错，需要关闭主分支master的保护，操作完成后，再开启主分支的保护机制。





### 如何消除：This branch is 23 commits ahead, 5 commits behind pingcap:master.以及下图中出现的一长串提交：

![image-20191106103256539](assets/image-20191106103256539.png)

1. cd 进入项目根目录，切换到 master 分支

   ```bash
   cd /Users/zhangjunlan/Documents/GitHub/docs
   # 切换到 master 分支
   git checkout master
   ```

2. 上游仓库 master 分支是最好的版本，所以将本地 master 分支强制和upstream master 同步

   ```bash
   # 从 upstream master 获取最新 HEAD
   git fetch upstream
   # 强制将当前 branch 与 upstream master 同步
   git reset --hard upstream/master
   ```

3. 将本地 master 分支强制推至 remote

   ```
   git push -f origin master
   ```

最后可以看到：This branch is even with pingcap:master