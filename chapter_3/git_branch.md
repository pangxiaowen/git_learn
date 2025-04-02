## 分支简述

Git 不是以一系列变更集或差异的形式存储数据，而是以一系列快照的形式存储数据。

当你进行提交时，Git 会存储一个提交对象，该对象包含指向你所暂存内容快照的指针。



## 创建新分支

git branch testing

查看分支指向

git log --oneline --decorate

## 切换分支

git checkout testing

git log 不会一直显示所有分支。如果您现在运行 git log，您可能会想知道您刚刚创建的 "testing" 分支去哪里了，因为它不会出现在输出中。

该分支并没有消失；Git 只是不知道您对该分支感兴趣，它试图向您展示它认为您感兴趣的东西。换句话说，默认情况下，git log 只会显示您已检出的分支以下的提交历史。

要显示所需分支的提交历史，您必须明确指定它：git log testing。要显示所有分支，请将 --all 添加到您的 git log 命令中。

git log --oneline --decorate --graph --all

从 Git 版本 2.23 开始，您可以使用 git switch 而不是 git checkout 来

切换到现有分支：git switch testing-branch。

创建一个新分支并切换到该分支：git switch -c new-branch。-c 标志代表创建，您也可以使用完整标志：--create。

返回到您之前检出的分支：git switch -。

