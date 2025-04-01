
### 看所有设置及其来源：
git config --list --show-origin

### 你的身份, 设置你的用户名和电子邮件地址
git config --global user.name "PXW"
git config --global user.email xxx@xx.com

### 您的编辑器, 您可以配置 Git 需要您输入消息时将使用的默认文本编辑器
git config --global core.editor vim

### 您的默认分支名称
Git 在您使用 git init 创建新存储库时会创建一个名为 master 的分支。 从 Git 版本 2.28 开始，您可以为初始分支设置不同的名称。 \

git config --global init.defaultBranch main

### 检查您的设置
可能会看到同一个键出现多次，在这种情况下，Git 将使用它看到的每个唯一键的最后一个值。

git config list
git config user.name