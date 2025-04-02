
您可以拥有多个远程仓库，每个远程仓库通常对您而言要么是只读的，要么是可读写的。与他人协作涉及管理这些远程仓库，并在需要共享工作时向其推送和拉取数据。

## 显示您的远程仓库

git remote 命令。它列出您指定的每个远程句柄的简称。如果您克隆了您的仓库，您应该至少看到 origin——这是 Git 为您克隆的服务器提供的默认名称。

git remove 

您还可以指定 -v，它会显示 Git 为简称存储的 URL，用于读取和写入该远程仓库。

git remove -v

## 添加远程仓库

可以在命令行中使用字符串 pb 代替整个 URL。 您可以运行 git fetch pb

git remote add pb https://github.com/paulboone/ticgit

git fetch pb

git push pb

## 从远程仓库获取和拉取

git fetch <remote>

该命令会连接到那个远程项目，并下载你还没有的所有数据。执行此操作后，你应该能够看到所有来自该远程项目的引用分支，你可以随时合并或检查它们。

git fetch 命令只会将数据下载到你的本地仓库，不会自动将其与你的任何工作合并或修改你当前正在处理的内容。当你准备好时，必须手动将其合并到你的工作中。

如果你的当前分支被设置为跟踪一个远程分支（请参阅下一节和Git 分支以获取更多信息），你可以使用git pull命令自动获取并将其合并到你的当前分支中。

## 推送到远程仓库

将你的master分支推送到你的origin服务器

git push origin master 

## 检查远程仓库

git remote show origin

## 重命名和删除远程仓库

git remote rename pb paul

git remote remove paul








