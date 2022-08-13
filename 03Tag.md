<!--
 * @FileName: 03Tag.md
 * @Author: Alen luojiaming299@163.com
 * @CreateTime: 2022-08-11 22:53:42
 * @LastEditTime: 2022-08-13 08:30:48
 * Copyright (c) 2022 by Alen, All Rights Reserved.
-->

# 创建标签
+ 命令 `git tag <tagname>` 用于新建一个标签，默认为 HEAD，也可以指定一个 commit id:
    ```bash
    $ git tag v0.9 f52c633
    ```
+ 命令 `git tag -a <tagname> -m "blablabla..."` 可以指定标签信息；
> 标签不是按时间顺序列出，而是按字母排序的。可以用 `git show <tagname>` 查看标签信息：
> ```
> $ git show v0.9
> ```
+ 命令 `git tag` 可以查看所有标签。

----------------------------------------------------------------

# 操作标签
+ 命令 git push origin <tagname> 可以推送一个本地标签；
+ 命令 git push origin --tags 可以推送全部未推送过的本地标签；
+ 命令 git tag -d <tagname> 可以删除未推送的一个本地标签；
+ 命令 git push origin :refs/tags/<tagname> 可以删除一个远程标签。
> 如果标签已经推送到远程，要删除远程标签先从本地删除：
> ```
> $ git tag -d v0.9
> ```
> 然后，从远程删除：
> ```
> $ git push origin :refs/tags/v0.9
> ```

