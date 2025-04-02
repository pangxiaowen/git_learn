## 基本分支与合并

如果您的工作目录或暂存区有未提交的更改，而这些更改与您要检出的分支冲突，则 Git 不会让您切换分支。

在切换分支时，最好保持一个干净的工作状态。有一些方法可以解决这个问题（主要是暂存和提交修改），我们将在后面的章节 暂存和清理 中介绍。

git checkout master

git merge testing

删除testing分支，因为您不再需要它

git branch -d testing

## 基本合并

git checkout master

git merge iss53

https://git-scm.cn/book/en/v2/Git-Branching-Basic-Branching-and-Merging


## 基本合并冲突

有时，此过程不会顺利进行。如果您在要合并的两个分支中以不同的方式更改了同一个文件的同一部分，Git 将无法干净地合并它们。

Git 没有自动创建新的合并提交。它在您解决冲突时暂停了此过程。如果您想在合并冲突后的任何时间查看哪些文件未合并，可以运行git status。

!!!!!!!!!!!!!!!! main