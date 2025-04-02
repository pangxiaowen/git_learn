## 分支简述

Git 不是以一系列变更集或差异的形式存储数据，而是以一系列快照的形式存储数据。

当你进行提交时，Git 会存储一个提交对象，该对象包含指向你所暂存内容快照的指针。



## 创建新分支

git branch testing

查看分支指向

git log --oneline --decorate

## 切换分支

git checkout testing
