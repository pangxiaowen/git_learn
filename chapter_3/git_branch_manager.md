## 分支管理

git branch 命令不仅仅创建和删除分支。如果您不带任何参数运行它，您将得到当前分支的简单列表。

注意 master 分支前缀的 * 字符：它指示您当前检出的分支（即 HEAD 指向的分支）。这意味着如果您此时提交，master 分支将随着您的新工作向前移动。

要查看每个分支上的最后一次提交，您可以运行 git branch -v。

此列表中前面没有 * 的分支通常可以使用 git branch -d 删除；您已经将它们的工作整合到另一个分支中，因此您不会丢失任何东西。

要查看所有包含您尚未合并的工作的分支，您可以运行 git branch --no-merged。

这将显示您的另一个分支。因为它包含尚未合并的工作，所以尝试使用 git branch -d 删除它将失败。

如果您确实想要删除分支并丢失这些工作，您可以使用 -D 强制删除，正如提示信息所指出的那样。

## 更改分支名称

不要重命名其他协作者仍在使用的分支。不要重命名诸如 master/main/mainline 之类的分支，除非您已阅读 更改 master 分支名称 部分。

假设您有一个名为 bad-branch-name 的分支，并且您想将其更改为 corrected-branch-name，同时保留所有历史记录。您还想在远程（GitHub、GitLab 或其他服务器）上更改分支名称。您该怎么做？

使用 git branch --move 命令在本地重命名分支。

git branch --move bad-branch-name corrected-branch-name

这将用 corrected-branch-name 替换您的 bad-branch-name，但这项更改目前仅在本地生效。要让其他人看到远程上的已更正分支，请将其推送到远程。

git push --set-upstream origin corrected-branch-name

现在我们将简要了解一下当前状态。
```
$ git branch --all
* corrected-branch-name
  main
  remotes/origin/bad-branch-name
  remotes/origin/corrected-branch-name
  remotes/origin/main
```

请注意，您位于 corrected-branch-name 分支上，并且它在远程可用。但是，带有错误名称的分支也仍然存在，但您可以通过执行以下命令将其删除。

git push origin --delete bad-branch-name

现在错误的分支名称已完全替换为已更正的分支名称。

## 更改 master 分支名称

更改像 master/main/mainline/default 这样的分支名称会破坏您的存储库使用的集成、服务、辅助实用程序和构建/发布脚本。在执行此操作之前，请务必与您的协作者协商。此外，请确保彻底搜索您的存储库，并在代码和脚本中更新对旧分支名称的所有引用。

使用以下命令将您的本地 master 分支重命名为 main

git branch --move master main

本地不再存在 master 分支，因为它已重命名为 main 分支。

要让其他人看到新的 main 分支，您需要将其推送到远程。这使得重命名的分支在远程可用

$ git push --set-upstream origin main

```
$ git branch --all
* main
  remotes/origin/HEAD -> origin/master
  remotes/origin/main
  remotes/origin/master
```
您的本地 master 分支已消失，因为它被 main 分支替换。main 分支存在于远程。但是，旧的 master 分支仍然存在于远程。其他协作者将继续使用 master 分支作为其工作的基础，直到您进行一些进一步的更改。

现在您面前还有几个任务需要完成转换
1. 任何依赖于此项目的项目都需要更新其代码和/或配置。
2. 更新任何测试运行器配置文件。
3. 调整构建和发布脚本。
4. 重定向存储库主机上的设置，例如存储库的默认分支、合并规则以及与分支名称匹配的其他内容。
5. 更新文档中对旧分支的引用。
6. 关闭或合并任何针对旧分支的拉取请求。

完成所有这些任务后，并且确定 main 分支的功能与 master 分支完全相同，您可以删除 master 分支

$ git push origin --delete master


