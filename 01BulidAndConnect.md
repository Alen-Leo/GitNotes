# 安装 git
```bash
$ sudo apt-get install git
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

----------------------------------------------------------------

# 初始化 git 仓库
```bash
$ git init
```

----------------------------------------------------------------

# 添加文件到 git 仓库
##### 分两步：
1. 使用命令 `git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令 `git commit -m <message>`，完成。
+ 要随时掌握工作区的状态，使用 `git status` 命令。
+ 如果 `git status` 告诉你有文件被修改过，用 `git diff` 可以查看修改内容。

----------------------------------------------------------------

# 版本回退
HEAD 指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令:
```bash
$ git reset --hard commit_id
```
穿梭前，用 `git log` 可以查看提交历史，以便确定要回退到哪个版本。
```
$ git log --pretty=oneline
```
要重返未来，用 `git reflog` 查看命令历史，以便确定要回到未来的哪个版本。

----------------------------------------------------------------

# 撤销修改
+ 场景 1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 `git checkout -- file`。
+ 场景 2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 git reset HEAD <file>，就回到了场景 1，第二步按场景 1 操作。
+ 场景 3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

----------------------------------------------------------------

# 删除文件
命令 `git rm` 用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

----------------------------------------------------------------

# 添加远程库
+ 第 1 步：安装 SSH 服务
    ```bash
    $ sudo apt-get install openssh-server
    ```
+ 第 2 步：创建 SSH Key
在用户主目录下，看看有没有 .ssh 目录，如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可直接跳到下一步。
如果没有，打开 Terminal，创建 SSH Key：
    ```bash
    $ ssh-keygen -t rsa -C "youremail@example.com"
    ```
+ 第 3 步：登陆远程仓库 *(GitHub, Gitee)*
Account settings——SSH Keys——Add SSH Key：在 Key 文本框里粘贴 id_rsa.pub 文件的内容
+ 第 4 步：远程仓库创建 repository 后，在本地的 learngit 仓库下运行命令：
    ```bash
    $ git remote add github git@github.com:Alen-Leo/GitStudy.git
    $ git remote add gitee git@gitee.com:alen-leo/imx6ull.git
    ```
+ 第 5 步：把本地库的所有内容推送到远程库上：
    ```bash
    $ git push -u origin master
    ```
> 把本地库的内容推送到远程，用 `git push` 命令，实际上是把当前分支 master 推送到远程。
> 由于远程库是空的，我们第一次推送 master 分支时，加上了 -u 参数，git 不但会把本地的 master 分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令。
> 从现在起，只要本地作了提交，就可以通过命令：
> ```bash
> $ git push origin master
> ```
> 如果推送失败，可以使用命令："`$ ssh -T git@github.com`" 测试连接状态。

----------------------------------------------------------------

# 删除库
如果添加的时候地址写错了，或者就是想删除远程库，可以用 `git remote rm <name>` 命令。
使用前，建议先用 `git remote -v` 查看远程库信息：
```bash
$ git remote -v
```
然后，根据名字删除，比如删除 origin：
```bash
$ git remote rm origin
```
> 此处的 “删除” 其实是解除了本地和远程的绑定关系，**并不是物理上删除了远程库**。远程库本身并没有任何改动。要真正删除远程库，需要登录到 GitHub，在后台页面找到删除按钮再删除。

-----------------------------------------------------------------

# 克隆库
远程库已经准备好了，下一步是用命令 `git clone` 从远程克隆一个本地库：
```bash
$ git clone git@github.com:michaelliao/gitskills.git
```



