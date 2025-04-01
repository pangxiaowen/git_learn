
## 撤销操作
常见的撤销操作之一发生在你过早提交时，可能忘记添加某些文件，或者提交信息出现错误。如果你想重做该提交，请进行你忘记的额外更改，暂存它们，然后使用 --amend 选项再次提交

git commit --amend

此命令获取你的暂存区并将其用于提交。如果你自上次提交以来没有进行任何更改（例如，你在上次提交后立即运行此命令），则你的快照看起来完全相同，你唯一更改的是提交信息。

例如，如果你提交后意识到忘记暂存想要添加到此提交中的某个文件中的更改，可以执行以下操作

```
$ git commit -m 'Initial commit'
$ git add forgotten_file
$ git commit --amend
```

## 取消暂存已暂存的文件

git reset chapter_2/main.cpp

git restore --staged chapter_2/main.cpp 

git reset可能是一个危险的命令，特别是如果您提供了--hard标志。 但是，在上面描述的场景中，工作目录中的文件不会被触碰，因此相对安全。


## 撤消已修改的文件

git checkout chapter_2/main.cpp

git checkout -- <file>是一个危险的命令。 您对该文件所做的任何本地更改都将消失——Git 只是用上次暂存或提交的版本替换了该文件。 除非您绝对知道不需要这些未保存的本地更改，否则请勿使用此命令

## 使用 git restore 撤消操作



