<!--
 * @FileName: 04SetUpTheServer.md
 * @Author: Alen luojiaming299@163.com
 * @CreateTime: 2022-08-11 22:53:42
 * @LastEditTime: 2022-08-13 09:31:20
 * Copyright (c) 2022 by Alen, All Rights Reserved.
-->

### 第一步 , 安装 git：
```
$ sudo apt-get install git
```
### 第二步, 创建一个 git 用户，用来运行 git 服务：
```
$ sudo adduser git
```
### 第三步, 创建证书登录：
收集所有需要登录的用户的公钥，就是他们自己的 id_rsa.pub 文件，把所有公钥导入到 "/home/git/.ssh/authorized_keys" 文件里，一行一个。
### 第四步, 初始化 Git 仓库：
先选定一个目录作为 Git 仓库，假定是 "/srv/sample.git"，在 / srv 目录下输入命令：
```
$ sudo git init --bare sample.git
```
Git 就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的 Git 仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区。
服务器上的 Git 仓库通常都以. git 结尾，把 owner 改为 git：
```
$ sudo chown -R git:git sample.git
```
### 第五步，禁用 shell 登录：
出于安全考虑，第二步创建的 git 用户不允许登录 shell，这可以通过编辑 / etc/passwd 文件完成。找到类似下面的一行：
```
git:x:1001:1001:,,,:/home/git:/bin/bash
```
改为：
```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```
这样，git 用户可以正常通过 ssh 使用 git，但无法登录 shell，因为我们为 git 用户指定的 git-shell 每次一登录就自动退出。
### 第六步，克隆远程仓库：
通过 `git clone` 命令克隆远程仓库了，在各自的电脑上运行：
```
$ git clone git@server:/srv/sample.git
```
## 管理公钥
如果团队很小，把每个人的公钥收集起来放到服务器的 "/home/git/.ssh/authorized_keys" 文件里就是可行的。
如果团队有几百号人，就没法这么玩了，这时，可以用 Gitosis 来管理公钥。
## 管理权限
因为 Git 是为 Linux 源代码托管而开发的，所以 Git 也继承了开源社区的精神，不支持权限控制。
不过，因为 Git 支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite 就是这个工具。
