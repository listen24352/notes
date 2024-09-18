[TOC]

# Git简介

> 源代码管理
>
> 方便多人协同开发
>
> 方便版本控制

## **工作区暂存区和仓库区**

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=ODU5MTVlZmExYTRmMGVkYWE5M2M3ZWRhNjM2OWMyNTVfODRENUZiRm1WWVMzY0pYc0w3anJyMlV5d0dzaWZSUjZfVG9rZW46QzRybWJOTjlib0QyYWx4VUhnc2M5QVlkbllkXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

#### **工作区**

- 对于`添加`、`修改`、`删除`文件的操作，都发生在工作区中

#### **暂存区**

- 暂存区指将工作区中的操作完成小阶段的存储，是版本库的一部分

#### **仓库区**

- 仓库区表示个人开发的一个小阶段的完成
  - 仓库区中记录的各版本是可以查看并回退的
  - 但是在暂存区的版本一旦提交就再也没有了

# Git单人本地仓库操作

### **ubuntu22.04 git操作**

#### 1.安装git

```Shell
sudo apt install git
```

#### 2.查看git版本

```SQL
leo@jammy:~$ git --version
git version 2.34.1
```

#### 3.创建目录

```Shell
leo@jammy:~$ cd Desktop/
leo@jammy:~/Desktop$ mkdir test
```

#### 4.初始化本地仓库

```Bash
leo@jammy:~/Desktop$ cd test/
leo@jammy:~/Desktop/test$ git init
提示：使用 'master' 作为初始分支的名称。这个默认分支名称可能会更改。要在新仓库中
提示：配置使用初始分支名，并消除这条警告，请执行：
提示：
提示：        git config --global init.defaultBranch <名称>
提示：
提示：除了 'master' 之外，通常选定的名字有 'main'、'trunk' 和 'development'。
提示：可以通过以下命令重命名刚创建的分支：
提示：
提示：        git branch -m <name>
已初始化空的 Git 仓库于 /home/leo/Desktop/test/.git/

# 配置使用初始分支名
leo@jammy:~/Desktop/test$ git config --global init.defaultBranch master
```

#### 5.配置个人信息

```Bash
leo@jammy:~/Desktop/test$ git config user.name 'leo'
leo@jammy:~/Desktop/test$ git config user.email 'leo@163.com'

# 查看配置信息
leo@jammy:~/Desktop/test$ cd .git/
leo@jammy:~/Desktop/test/.git$ ls
branches  config  description  HEAD  hooks  info  objects  refs
leo@jammy:~/Desktop/test/.git$ cat config 
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[user]
        name = leo
        email = leo@163.com
```

#### 6.新建login.py文件

```Bash
leo@jammy:~/Desktop/test$ touch login.py
```

#### 7.查看文件状态

> - 红色表示新建文件或者新修改的文件,都在工作区.
> - 绿色表示文件在暂存区
> - 新建的`login.py`文件在工作区，需要添加到暂存区并提交到仓库区

```Bash
leo@jammy:~/Desktop/test$ git status
```

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=NDI4ZTllY2RhNWQ1ZmZmM2IzZDg1ZTQwNzEwM2M0ZTlfUzhYNVI0Z2FXbWNHbUlJTkhpR3hqWG43YkhBcGpPTzZfVG9rZW46VGNXN2IwWUpFb0xKZGx4aExjQ2NJM0lXblFlXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

#### 8.将工作区文件添加到暂存区

```Bash
  # 添加项目中所有文件
  git add .
  或者
  # 添加指定文件
  git add login.py
```

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=YWYyOTM0YmMxNzk0YzRiZjM4MjcwOWNkZGYzODFmY2NfcUVHS2hhc2N0bzdycHVwblU1UVZhQmJiNnJMMDFvdnFfVG9rZW46R0g5bmJwR01Tb01wbEF4dkIxV2NlYW1lbkVlXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

#### 取消暂存（从暂存区恢复到工作区）

```Bash
git rm --cached <文件>...
```

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=OTdjY2ZlODM2YWYyMzUyNzc2ZWE2M2E0NTFiODk3YmZfOURTeTI4MVVZTW8wRTc2eklmT0JnN1RabHo4d0hDeTNfVG9rZW46TW5FNGJkbDlLb2t6Nkd4RWVLQmNaelFhbmxoXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

#### 9.将暂存区文件提交到仓库区

> - `commit`会生成一条版本记录
> - `-m`后面是版本描述信息
> - **39c39c3---版本号**

```Bash
leo@jammy:~/Desktop/test$ git commit -m '版本描述'
[master （根提交） 39c39c3] 版本描述
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 login.py

leo@jammy:~/Desktop/test$ git status
位于分支 master
无文件要提交，干净的工作区
```

#### 10.编写login.py

> - 代码编辑完成后即可进行`add`和`commit`操作
> - 提示：添加和提交合并命令
>
> ```Plaintext
>   git commit -am "版本描述"
> ```

```Bash
leo@jammy:~/Desktop/test$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     login.py

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）


leo@jammy:~/Desktop/test$ git commit -am '添加一个函数'
[master 745e228] 添加一个函数
 1 file changed, 4 insertions(+)
```

#### 11.查看历史版本

> git reflog 
>
> **可以查看所有分支的所有操作记录（包括commit和reset的操作），包括已经被删除的commit记录** git log 
>
> **则不能察看已经删除了的commit记录**

```Bash
leo@jammy:~/Desktop/test$ git log
# 版本号
commit 745e2284fcdc4db917eef3c764db67b985622166 (HEAD -> master)
# 提交人
Author: leo <leo@163.com>
# 提交时间
Date:   Mon Apr 29 09:08:40 2024 +0800
    # 版本描述
    添加一个函数

commit 39c39c376a3f5fb74608012822b0e615500f68a9
Author: leo <leo@163.com>
Date:   Mon Apr 29 08:59:58 2024 +0800

    版本描述
    
    
leo@jammy:~/Desktop/test$ git reflog 
745e228 (HEAD -> master) HEAD@{0}: commit: 添加一个函数
39c39c3 HEAD@{1}: commit (initial): 版本描述
```

**查看提交历史及分支图**：

```Bash
git log --graph --all --decorate --oneline
```

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=MTQzYmYwNDVhODlmNmY2MDczOTI4MTA5YzljMzJhZmZfZDZ3UW5NeVNMeEFFM1ZacG9xSFEwWDFhNnlsdlhzZVBfVG9rZW46VzJTMWI5SHNMb0s2MUJ4SVJWd2M3WGQ3bmxIXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

#### 12.回退版本

##### 方案一

> 通过每个版本的版本号回退到指定版本

```Bash
  git reset --hard 版本号
leo@jammy:~/Desktop/test$ cat login.py 
def demo_git():
    return 'Hello Git!!!'

print(demo_git())



class Git:
    pass

leo@jammy:~/Desktop/test$ git reset --hard 745e228
HEAD 现在位于 745e228 添加一个函数
leo@jammy:~/Desktop/test$ cat login.py 
def demo_git():
    return 'Hello Git!!!'

print(demo_git())
```

##### 方案二

- `HEAD`表示当前最新版本
- `HEAD^`表示当前最新版本的前一个版本
- `HEAD^^`表示当前最新版本的前两个版本，**以此类推...**
- `HEAD~1`表示当前最新版本的前一个版本
- `HEAD~10`表示当前最新版本的前10个版本，**以此类推...**

```Bash
git reset --hard HEAD^
leo@jammy:~/Desktop/test$ git reset --hard HEAD
HEAD 现在位于 745e228 添加一个函数
leo@jammy:~/Desktop/test$ git reset --hard HEAD^  # 回退一个版本
HEAD 现在位于 39c39c3 版本描述
leo@jammy:~/Desktop/test$ git reset --hard 6028561
HEAD 现在位于 6028561 添加一个类
leo@jammy:~/Desktop/test$ git reset --hard HEAD^^  # 回退二个版本
HEAD 现在位于 39c39c3 版本描述


leo@jammy:~/Desktop/test$ git reset --hard HEAD~1  # 回退一个版本
HEAD 现在位于 745e228 添加一个函数
leo@jammy:~/Desktop/test$ git reset --hard 6028561
HEAD 现在位于 6028561 添加一个类
leo@jammy:~/Desktop/test$ git reset --hard HEAD~2  # 回退二个版本
HEAD 现在位于 39c39c3 版本描述
```

#### 13.撤销修改

- 只能撤销工作区、暂存区的代码,不能撤销仓库区的代码
- 撤销仓库区的代码就相当于回退版本操作
- git checkout -- <file>  这个操作是不可逆的

#####  撤销工作区的代码

```Python
leo@jammy:~/Desktop/test$ cat login.py 
def demo_git():
    return 'Hello Git!!!'

print(demo_git())


class Git:
    pass


def checkout():
    """工作区撤销修改"""
    pass

leo@jammy:~/Desktop/test$ git status
位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     login.py

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
leo@jammy:~/Desktop/test$ 
leo@jammy:~/Desktop/test$ git checkout login.py
从索引区更新了 1 个路径
leo@jammy:~/Desktop/test$ cat login.py 
def demo_git():
    return 'Hello Git!!!'

print(demo_git())
```

##### 撤销暂存区代码

```Bash
leo@jammy:~/Desktop/test$ git reset HEAD login.py
重置后取消暂存的变更：
M        login.py

leo@jammy:~/Desktop/test$ git checkout login.py
从索引区更新了 1 个路径
```

# Git远程仓库Github

### 1.创建远程仓库

### 2.配置SSH

[生成新的 SSH 密钥并将其添加到 ssh-agent - GitHub 文档](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```Bash
ssh-keygen -t ed25519 -C "your_email@example.com"

Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/lighthouse/.ssh/id_ed25519): 

Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 

Your identification has been saved in /home/lighthouse/.ssh/id_ed25519

Your public key has been saved in /home/lighthouse/.ssh/id_ed25519.pub

The key fingerprint is:
SHA256:FnvDP1PsSdtnfSgHFrQov6NEVkOgZv0V6ZcueiorkEg listen24352@163.com
The key's randomart image is:
+--[ED25519 256]--+
|        ... o.   |
|       o . o.o   |
|      + + +.+  . |
|  E  o   O o.oo  |
| . . .  S * oo+  |
|  . o  + . =.=.=.|
|     .  . o.=.* *|
|      .......= .o|
|       .oo.o     |
+----[SHA256]-----+
```

测试 ssh -T git@github.com Hi listen24352! You've successfully authenticated, but GitHub does not provide shell access.

### 3.克隆项目

#### manager

```Bash
cd Desktop
mkdir git
cd git
mkdir leo
mkdir manager

cd manager
git clone git@github.com:listen24352/study_git.git
cd study_git

git config user.name 'manager'
git config user.email 'manager@qq.com'

mkdir test
touch login.py

git add .
git commit -m '立项'
git push
```

#### Leo

```Bash
cd leo
git clone git@github.com:listen24352/study_git.git
cd study_git

git config user.name 'leo'
git config user.email 'leo@qq.com'
```

### 4.多人协同开发

#### Leo 

```Python
cd leo/study_git 
Vim home.py

def register():
    """注册"""
    print("注册成功")

git add .
git commit -m 'register'
git push
```

#### Manager

```Python
cd manager/study_git
git pull

vim home.py
def login():
    """登录"""
    print('登录成功')

# 没有添加新文本
git commit -am 'login'
git push
```

#### Leo

```Python
cd leo/study_git 
# 同步服务器代码
git pull
```

#### 总结

> - 循环操作，协同开发
> - 要使用git命令操作仓库，需要进入到仓库内部
> - 要同步服务器代码就执行：`git pull`
> - 本地仓库记录版本就执行：`git commit -am '版本描述'`
> - 推送代码到服务器就执行：`git push`
> - 编辑代码前要先`pull`，编辑完再`commit`，最后推送是`push`

### 5.代码冲突

> - **提示**：多人协同开发时，避免不了会出现代码冲突的情况
> - **原因**：多人同时修改了同一个文件
> - **危害**：会影响正常的开发进度
> - **注意**：一旦出现代码冲突，必须先解决再做后续开发

#### 制造冲突

Leo

```Python
cd leo/study_git 
Vim dev.py

# 添加代码
a = '制造冲突'

git commit -am '制造冲突'
git push
```

Manager 

```Python
cd manager/study_git

vim dev.py

def manager():
    a = '制造冲突'



git commit -am '制造冲突manager'
[main 4b3b55c] 制造冲突manager
 1 file changed, 5 insertions(+)

git push
To github.com:listen24352/study_git.git
 ! [rejected]        main -> main (fetch first)
error: 无法推送一些引用到 'github.com:listen24352/study_git.git'
提示：更新被拒绝，因为远程仓库包含您本地尚不存在的提交。这通常是因为另外
提示：一个仓库已向该引用进行了推送。再次推送前，您可能需要先整合远程变更
提示：（如 'git pull ...'）。
提示：详见 'git push --help' 中的 'Note about fast-forwards' 小节。



leo@jammy:~/Desktop/git/manager/study_git/test$ git pull
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 4 (delta 1), pack-reused 0
展开对象中: 100% (4/4), 394 字节 | 98.00 KiB/s, 完成.
来自 github.com:listen24352/study_git
   5b1e293..3a5a81c  main       -> origin/main
提示：您有偏离的分支，需要指定如何调和它们。您可以在执行下一次
提示：pull 操作之前执行下面一条命令来抑制本消息：
提示：
提示：  git config pull.rebase false  # 合并（缺省策略）
提示：  git config pull.rebase true   # 变基
提示：  git config pull.ff only       # 仅快进
提示：
提示：您可以将 "git config" 替换为 "git config --global" 以便为所有仓库设置
提示：缺省的配置项。您也可以在每次执行 pull 命令时添加 --rebase、--no-rebase，
提示：或者 --ff-only 参数覆盖缺省设置。
fatal: 需要指定如何调和偏离的分支。
```

#### 解决冲突

```Python
leo@jammy:~/Desktop/git/leo/study_git/test$ cat login.py 
def demo_git():
    return 'Hello Git!!!'
<<<<<<< HEAD  冲突区域通常会被特殊的标记包围
=======

print(demo_git())



class Git:
    pass

print(abs(-1))
>>>>>>> 4a7845d (abs)
git config pull.rebase false
git pull
自动合并 test/dev.py
冲突（内容）：合并冲突于 test/dev.py
自动合并失败，修正冲突然后提交修正的结果。

删掉冲突代码

git commit -am '解决冲突'
git push
NOTE ABOUT FAST-FORWARDS  快进注意事项
    When an update changes a branch (or more in general, a ref) that used to point at commit A to point at another commit B, it is called a fast-forward update if and only if B is a descendant of A.
    当更新将一个分支(或者更一般地说，一个ref)从指向提交a更改为指向另一个提交B时，当且仅当B是a的后代时，它被称为快进更新。

    In a fast-forward update from A to B, the set of commits that the original commit A built on top of is a subset of the commits the new commit B builds on top of. Hence, it does not lose any history.
    在从a到B的快速更新中，构建在原始提交a之上的提交集是构建在新提交B之上的提交的子集。因此，它不会丢失任何历史。

    In contrast, a non-fast-forward update will lose history. For example, suppose you and somebody else started at the same commit X, and you built a history leading to commit B while the other person built a history leading to commit A. The history looks like this:
    相反，非快进更新将丢失历史记录。例如，假设你和另一个人从同一个提交X开始，你创建了一个提交B的历史记录，而另一个人创建了一个提交a的历史记录，历史记录是这样的:
                 B
                /
            ---X---A
    Further suppose that the other person already pushed changes leading to A back to the original repository from which you two obtainedthe original commit X.
    进一步假设另一个人已经将导致A的更改推回了原始存储库，你们两个从中获得了原始提交X。
    
    The push done by the other person updated the branch that used to point at commit X to point at commit A. It is a fast-forward.
    由另一个人完成的推送将过去指向提交X的分支更新为指向提交a的分支，这是一个快进。

    But if you try to push, you will attempt to update the branch (that now points at A) with commit B. This does not fast-forward. If you did so, the changes introduced by commit A will be lost, because everybody will now start building on top of B.
    但是，如果您尝试推送，您将尝试用提交b更新分支(现在指向A)。这不会快进。如果这样做，提交A所引入的更改将丢失，因为现在每个人都将开始在B的基础上进行构建。
    
    The command by default does not allow an update that is not a fast-forward to prevent such loss of history.
    默认情况下，该命令不允许非快进的更新，以防止此类历史记录丢失。

    If you do not want to lose your work (history from X to B) or the work by the other person (history from X to A), you would need to first fetch the history from the repository, create a history that contains changes done by both parties, and push the result back.
    如果您不想丢失您的工作(从X到B的历史记录)或其他人的工作(从X到A的历史记录)，则需要首先从存储库中获取历史记录，创建包含双方所做更改的历史记录，并将结果发回。
    
    You can perform "git pull", resolve potential conflicts, and "git push" the result. A "git pull" will create a merge commit C between commits A and B.
    你可以执行“git pull”，解决潜在的冲突，然后“git push”结果。“git pull”会在提交A和提交B之间创建一个合并提交C。
    
                B---C
                /   /
            ---X---A

    Updating A with the resulting merge commit will fast-forward and your push will be accepted.
    使用合并提交结果更新A将快速前进，并且您的推送将被接受。

    Alternatively, you can rebase your change between X and B on top of A, with "git pull --rebase", and push the result back. The rebase will create a new commit D that builds the change between X and B on top of A.
    或者，您可以使用“git pull --rebase”将X和B之间的更改重新置于A之上，然后将结果推回去。rebase将创建一个新的提交D，在a的基础上构建X和B之间的更改。
                 B   D
                /   /
            ---X---A

    Again, updating A with this commit will fast-forward and your push will be accepted.
    同样，使用此提交更新A将快速前进，并且您的推送将被接受。
    
    There is another common situation where you may encounter non-fast-forward rejection when you try to push, and it is possible even whenyou are pushing into a repository nobody else pushes into. After you push commit A yourself (in the first picture in this section),
replace it with "git commit --amend" to produce commit B, and you try to push it out, because forgot that you have pushed A out already. In such a case, and only if you are certain that nobody in the meantime fetched your earlier commit A (and started building on top of it), you can run "git push --force" to overwrite it. In other words, "git push --force" is a method reserved for a case where you do mean to lose history.
    还有另一种常见的情况是，当您尝试推进时，可能会遇到非快速推进的拒绝，甚至当您推进到没有其他人推进的存储库时也是可能的。在你自己推送提交A之后(在本节的第一张图片中)，
将其替换为“git commit --amend”以生成提交B，并且您试图推出它，因为忘记了您已经推出了A。在这种情况下，只有当您确定没有人同时获取您先前的提交a(并开始在其上构建)时，您才能运行“git push --force”来覆盖它。换句话说，“git push --force”是为您确实想要丢失历史记录的情况保留的方法。
```

#### **补充：**

- **容易冲突的操作方式**
  - 多个人同时操作了同一个文件
  - 一个人一直写不提交
  - 修改之前不更新最新代码
  - 提交之前不更新最新代码
  - 擅自修改同事代码
- **减少冲突的操作方式**
  - 养成良好的操作习惯,先`pull`在修改,修改完立即`commit`和`push`
  - 一定要确保自己正在修改的文件是最新版本的
  - 各自开发各自的模块
  - 如果要修改公共文件,一定要先确认有没有人正在修改
  - 下班前一定要提交代码,上班第一件事拉取最新代码
  - 一定不要擅自修改同事的代码

### 6.分支

- 作用：
  - 区分生产环境代码以及开发环境代码
  - 研究新的功能或者攻关难题
  - 解决线上bug
- 特点：
  - 项目开发中公用分支包括main、dev
  - 分支main是默认分支，用于发布，当需要发布时将dev分支合并到main分支
  - 分支dev是用于开发的分支，开发完阶段性的代码后，需要合并到main分支

#### Manager

```Python
# 1.进入到经理的本地仓库
cd manager/study_git

# 2.查看当前分支
git branch 
* main

# 3.经理创建并切换到dev分支
git checkout -b dev
切换到一个新分支 'dev'

# 4.设置本地分支跟踪远程指定分支（将分支推送到远程）
git push --set-upstream origin dev

# 5.经理在dev分支编辑代码
vim dev.py
def dev():
    print('dev分支')

# 6.管理dev分支源代码：add、commit、push
git add .
git commit -m 'dev'
git push

# 7.dev分支合并到main分支
# 提示：只有当dev分支合并到master分支成功，leo才能获取到最新代码 或者
# 1.切换主分支
git switch main
# 2.dev分支合并到main分支
git merge dev
# 3.合并分支默认在本地完成，合并后直接推送
git push
```

#### Leo

```Bash
cd leo/study_git
# 同步服务器代码
git pull
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 1), reused 4 (delta 1), pack-reused 0
展开对象中: 100% (4/4), 356 字节 | 89.00 KiB/s, 完成.
来自 github.com:listen24352/study_git
   f7beebc..5b1e293  main       -> origin/main
 * [新分支]          dev        -> origin/dev
更新 f7beebc..5b1e293
Fast-forward
 test/dev.py | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 test/dev.py
```

### 7.标签

> - 当某一个大版本完成之后,需要打一个标签
> - 作用：
>   - 记录大版本
>   - 备份大版本代码

#### Manager

```Python
# 1.进入到经理的本地仓库
cd manager/study_git

# 2.经理在本地打标签
# git tag -a 标签名 -m '标签描述'
git tag -a 1.0 -m '标签'

# 3.经理推送标签到远程仓库
# git push origin 标签名
git push origin 1.0
枚举对象中: 1, 完成.
对象计数中: 100% (1/1), 完成.
写入对象中: 100% (1/1), 156 字节 | 156.00 KiB/s, 完成.
总共 1（差异 0），复用 0（差异 0），包复用 0
To github.com:listen24352/study_git.git
 * [new tag]         1.0 -> 1.0
```

4.github查看标签

![img](https://px60te123t5.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjA0NzgwYjBkMzBhYWY1NWRmMjEwMzcwODQyOTFhNzhfUVN4cWs4c1ZIV0ZQNm11RDN6VXlkS1NFbGU0bnNOaGlfVG9rZW46RUVQTGJOOENOb3JLazN4eVdmR2MwMkJpbkJnXzE3MjY2MjcwMzg6MTcyNjYzMDYzOF9WNA)

5.删除本地和远程标签

```Python
# 删除本地标签
git tag -d <tagname>...


# 删除远程标签
git push origin --delete tag <tagname>...
```

# 进阶

```
git pull --rebase 是一个 Git 命令，它结合了 git fetch 和 git rebase 的功能。下面我将详细解释这条命令的各个部分：
git pull:
git pull 是从另一个存储库或本地分支获取并集成（整合）更改的命令。
默认情况下，git pull 会执行一个 git fetch（从远程获取最新的更改，但不合并或应用它们）和一个 git merge（将远程的更改合并到当前分支）。
--rebase:
当使用 --rebase 选项时，git pull 将不再执行 git merge，而是执行 git rebase。
git rebase 的主要目的是将一个分支上的所有提交重新应用到另一个分支上。
与 git merge 不同，git rebase 会尝试保留一个线性提交历史。它取出你在当前分支上的所有提交，保存为临时文件，然后更新你当前分支的基准点（即你上一次从另一个分支拉取代码时的位置），最后把你的提交逐一重新应用上去。
使用 git pull --rebase 的好处是：
保持提交历史的清晰：与 git merge 可能会引入一个合并提交不同，git rebase 会保持一个线性的提交历史，这使得查看和理解项目的历史变得更加容易。
避免不必要的合并提交：如果你经常与远程分支同步，使用 git rebase 可以避免产生大量的合并提交，从而保持提交历史的整洁。
```