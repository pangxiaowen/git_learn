## 获取 Git 仓库

通常，获取 Git 仓库有两种方法：
1. 你可以将一个当前未受版本控制的本地目录转换为 Git 仓库，或者
2. 你可以从其他地方克隆一个现有的 Git 仓库。

### 在现有目录中初始化仓库
git init
git add chapter_2/main.cpp
git commit -m 'Initial project version'

### 克隆现有仓库
Git 获取的不仅仅是一个工作副本，而是服务器上几乎所有数据的完整副本。当你运行git clone时，默认情况下会下载项目历史记录中每个文件的每个版本。

git clone https://github.com/libgit2/libgit2    

如果你想将仓库克隆到除libgit2之外的其他目录中，可以指定新的目录名称作为附加参数 

git clone https://github.com/libgit2/libgit2 mylibgit

## 记录仓库中的更改

工作目录中的每个文件都可以处于两种状态之一：已跟踪或未跟踪。已跟踪文件是指上次快照中的文件，以及任何新暂存的文件；它们可以是未修改的、已修改的或已暂存的。简而言之，已跟踪文件是Git知道的文件。

未跟踪文件是其他所有内容——工作目录中不在上次快照中且不在暂存区域中的任何文件。当您首次克隆一个仓库时，所有文件都将被跟踪且未修改，因为Git刚刚检出它们，并且您还没有编辑任何内容。

### 检查文件状态
git status

### 跟踪新文件
git add命令接受文件或目录的路径名；如果是目录，则该命令会递归地添加该目录中的所有文件。

git add README

### 暂存已修改的文件

git add chapter_2/git_base.md

## 简短状态
git status -s
git status --short

## 忽略文件
cat .gitignore

您可以放在.gitignore文件中的模式规则如下
1. 空行或以#开头的行将被忽略。
2. 标准的 glob 模式有效，并将递归地应用于整个工作树。
3. 您可以以正斜杠（/）开头模式以避免递归。
4. 您可以以正斜杠（/）结尾模式以指定目录。
5. 您可以通过在模式开头使用感叹号（!）来否定模式。

Glob 模式类似于 shell 使用的简化正则表达式。
* 星号（*）匹配零个或多个字符；
* [abc]匹配括号内的任何字符（在本例中为 a、b 或 c）；问号（?）匹配单个字符；
* 括号括起来的字符之间用连字符分隔（[0-9]）匹配它们之间的任何字符（在本例中为 0 到 9）。
* 您还可以使用两个星号来匹配嵌套目录；a/**/z将匹配a/z、a/b/z、a/b/c/z等。

在简单的情况下，仓库在其根目录中可能只有一个.gitignore文件，该文件递归地应用于整个仓库。但是，也可以在子目录中添加其他.gitignore文件。这些嵌套的.gitignore文件中的规则仅适用于它们所在的目录下的文件。

## 查看已暂存和未暂存的更改

git diff本身不会显示自上次提交以来所做的所有更改——仅显示仍未暂存的更改。

### 要查看您已更改但尚未暂存的内容

git diff

git diff chapter_2/git_base.md

### 如果您想查看已暂存的内容

git diff --staged
git diff --cached

## 提交更改

git commit

git commit -m "!!!!!!!"

提交记录了您在暂存区中设置的快照。您未暂存的任何内容仍然存在并被修改；您可以进行另一个提交以将其添加到您的历史记录中。每次执行提交时，您都记录了项目的快照，以后可以恢复或比较该快照。

## 跳过暂存区

git commit命令添加-a选项会使 Git 在执行提交之前自动暂存所有已跟踪的文件，从而使您可以跳过git add部分

git commit -a -m "!!!!!!!!!!!"

## 删除文件

要从 Git 中删除文件，您必须将其从跟踪的文件中删除（更准确地说，将其从暂存区中删除），然后提交。git rm命令执行此操作，还会从您的工作目录中删除文件，因此下次您不会将其视为未跟踪的文件。

如果您只是从工作目录中删除文件，它会显示在git status输出的“未暂存以提交的更改”（即未暂存）区域中

如果您运行git rm，它将暂存文件的删除操作

下次您提交时，该文件将消失且不再被跟踪。如果您修改了文件或已将其添加到暂存区，则必须使用-f选项强制删除。这是一项安全功能，可以防止意外删除尚未记录在快照中且无法从 Git 中恢复的数据。

您可能想要做的另一件有用的事情是将文件保留在您的工作树中，但将其从您的暂存区中删除。换句话说，您可能希望将文件保留在硬盘驱动器上，但不再让 Git 跟踪它。果您忘记将某些内容添加到您的.gitignore文件中并意外地将其暂存，例如大型日志文件或一堆.a编译文件，这将特别有用。为此，请使用--cached选项

git rm --cached README

git rm -f README

## 移动文件
Git 中重命名文件

git mv a b

这等效于运行以下命令

1. mv a b
2. git rm a
3. git add b
