<!--
 * @FileName: 02Branch.md
 * @Author: Alen luojiaming299@163.com
 * @CreateTime: 2022-08-11 22:53:42
 * @LastEditTime: 2022-08-13 09:30:24
 * Copyright (c) 2022 by Alen, All Rights Reserved.
-->

# 分支管理
查看分支：`git branch`
创建分支：`git branch <name>`
切换分支：`git checkout <name>` 或者 `git switch <name>`
创建/切换分支：`git checkout -b <name>` 或者 `git switch -c <name>`
合并某分支到当前分支：`git merge <name>`
删除分支：`git branch -d <name>`

----------------------------------------------------------------

# 解决冲突
当 git 无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把 git 合并失败的文件手动编辑为我们希望的内容，再提交。
用 `git log --graph` 命令可以看到分支合并图。

----------------------------------------------------------------

# 分支管理策略
Git 分支十分强大，在团队开发中应该充分应用。
合并分支时，加上 `--no-ff` 参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而 fast forward 合并就看不出来曾经做过合并。

----------------------------------------------------------------

# Bug 分支
修复 bug 时，我们会通过创建新的 bug 分支进行修复，然后合并，最后删除。
当手头工作没有完成时，先把工作现场 `git stash` 一下，然后去修复 bug，修复后，工作区是干净的，可以用 `git stash list` 命令查看原来的工作现场：
```bash
$ git stash list
stash@{0}: WIP on dev: f52c633 add merge
```
有两个办法恢复：
+ 一是用 `git stash apply` 恢复，但是恢复后，stash 内容并不删除，你需要用 `git stash drop` 来删除；
+ 另一种方式是用 `git stash pop`，恢复的同时把 stash 内容也删了。
> 可以多次 stash，恢复的时候，先用 `git stash list` 查看，然后恢复指定的 *stash*，用命令：
> ```bash
> $ git stash apply stash@{0}
> ```
在 master 分支上修复的 bug，想要合并到当前 dev 分支，可以用 `git cherry-pick <commit>` 命令，把 bug 提交的修改 “复制” 到当前分支，避免重复劳动。
```bash
$ git cherry-pick 4c805e2
```

----------------------------------------------------------------

# 删除未合并分支
要删除一个没有被合并过的分支，可以通过 `git branch -D <name>` 强行删除。

----------------------------------------------------------------

# 多人协作
+ 查看远程库信息，使用 `git remote -v`；
+ 本地新建的分支如果不推送到远程，对其他人就是不可见的；
+ 从本地推送分支，使用 `git push origin branch-name`，如果推送失败，则因为远程分支比你的本地更新，需要先用 `git pull` 抓取远程的新提交，如果合并有冲突，则解决冲突，并在本地提交；
+ 在本地创建和远程分支对应的分支，使用 `git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
+ 建立本地分支和远程分支的关联，使用 `git branch --set-upstream branch-name origin/branch-name`；
> 如果 `git pull` 提示 "no tracking information"，则说明本地分支和远程分支的链接关系没有创建，用命令 `git branch --set-upstream-to <branch-name> origin/<branch-name>`。
+ 从远程抓取分支，使用 `git pull`，如果有冲突，要先处理冲突。

----------------------------------------------------------------

# rebase 操作
+ rebase 操作可以把本地未 push 的分叉提交历史整理成直线；
+ rebase 的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。












