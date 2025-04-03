## 远程分支

远程引用是在您的远程仓库中的引用（指针），包括分支、标签等。您可以使用 git ls-remote <remote> 显式获取远程引用的完整列表，或者使用 git remote show <remote> 获取远程分支以及更多信息。但是，更常见的方法是利用远程跟踪分支。

远程跟踪分支是对远程分支状态的引用。它们是本地引用，您无法移动它们；当您执行任何网络通信时，Git 会为您移动它们，以确保它们准确地表示远程仓库的状态。可以将它们视为书签，以提醒您上次连接到远程仓库时分支所在的位置。

就像分支名称“master”在 Git 中没有任何特殊含义一样，“origin” 也没有。虽然“master”是运行 git init 时起始分支的默认名称，这是它被广泛使用的原因，但“origin”是运行 git clone 时远程仓库的默认名称。如果您改为运行 git clone -o booyah，那么您将拥有 booyah/master 作为您的默认远程分支。

### 推送

当你想要与世界共享一个分支时，你需要将其推送到你有写入权限的远程服务器上。你的本地分支不会自动与你写入的远程服务器同步——你必须显式推送要共享的分支。这样，你可以使用私有分支进行不想共享的工作，并且仅推送要协作的主题分支。

如果你有一个名为 serverfix 的分支，想要与其他人一起处理，你可以像推送第一个分支一样推送它。运行 git push <remote> <branch>

git push origin serverfix

这是一个捷径。Git 会自动将 serverfix 分支名称扩展为 refs/heads/serverfix:refs/heads/serverfix，这意味着：“获取我的 serverfix 本地分支并将其推送以更新远程的 serverfix 分支。

你也可以执行 git push origin serverfix:serverfix，它执行相同的操作——它表示：“获取我的 serverfix 并将其设为远程的 serverfix。” 你可以使用此格式将本地分支推送到名称不同的远程分支。

如果你不希望它在远程服务器上称为 serverfix，则可以运行 git push origin serverfix:awesomebranch 将你的本地 serverfix 分支推送到远程项目的 awesomebranch 分支。

如果你不想每次推送都输入密码，可以设置“凭据缓存”。最简单的方法是将其保留在内存中几分钟，你可以通过运行 git config --global credential.helper cache 来轻松设置。

下次你的某个协作者从服务器获取数据时，他们将获得一个指向服务器上 serverfix 版本在远程分支 origin/serverfix 下的位置的引用。

git fetch origin

需要注意的是，当你执行获取操作以下载新的远程跟踪分支时，你不会自动拥有它们的本地可编辑副本。换句话说，在这种情况下，你没有新的 serverfix 分支——你只有无法修改的 origin/serverfix 指针。

要将此工作合并到你的当前工作分支中，你可以运行 git merge origin/serverfix。如果你想要自己的 serverfix 分支以供处理，可以基于你的远程跟踪分支创建它。

git checkout -b serverfix origin/serverfix

这会为你提供一个你可以处理的本地分支，该分支从 origin/serverfix 的位置开始。

## 跟踪分支

从远程跟踪分支检出本地分支会自动创建一个所谓的“跟踪分支”（它跟踪的分支称为“上游分支”）。跟踪分支是与远程分支具有直接关系的本地分支。如果你位于跟踪分支上并键入 git pull，Git 会自动知道要从哪个服务器获取数据以及要合并哪个分支。

当你克隆存储库时，它通常会自动创建一个跟踪 origin/master 的 master 分支。但是，如果你愿意，可以设置其他跟踪分支——那些跟踪其他远程服务器上的分支或不跟踪 master 分支的分支。

git checkout --track origin/serverfix

事实上，这个操作如此常见，以至于还有一个快捷方式。如果要检出的分支名称 (a) 不存在，并且 (b) 与唯一一个远程服务器上的名称完全匹配，Git 将为你创建一个跟踪分支。

要设置与远程分支名称不同的本地分支，可以轻松地使用第一个版本并使用不同的本地分支名称。

git checkout -b sf origin/serverfix

现在，你的本地分支 sf 将自动从 origin/serverfix 获取数据。

如果你已经有一个本地分支，并且想要将其设置为刚刚拉取的远程分支，或者想要更改正在跟踪的上游分支，可以在任何时候使用 git branch 的 -u 或 --set-upstream-to 选项显式设置它。

git branch -u origin/serverfix

如果你想查看设置了哪些跟踪分支，可以使用 git branch 的 -vv 选项。这将列出你的本地分支，并提供更多信息，包括每个分支正在跟踪什么以及你的本地分支是领先、落后还是两者兼而有之。

## 拉取

虽然 git fetch 命令会获取服务器上你还没有的所有更改，但它不会修改你的工作目录。它只会获取数据并让你自己合并。但是，有一个名为 git pull 的命令，在大多数情况下，它本质上是 git fetch 后紧跟 git merge。如果你设置了跟踪分支（如上一节中所示），无论是通过显式设置还是通过 clone 或 checkout 命令为你创建，git pull 将查找你的当前分支正在跟踪哪个服务器和分支，从该服务器获取数据，然后尝试合并该远程分支。

通常，最好简单地显式使用 fetch 和 merge 命令，因为 git pull 的“魔力”通常会令人困惑。

## 删除远程分支

假设你已完成远程分支——例如，你和你的协作者已完成某个功能，并将其合并到远程服务器的 master 分支（或你的稳定代码行所在的任何分支）中。你可以使用 git push 的 --delete 选项删除远程分支。如果你想从服务器删除 serverfix 分支，可以运行以下命令：

$ git push origin --delete serverfix