## 签名你的工作

### GPG 简介

首先，如果你想要签署任何内容，你需要配置 GPG 并安装你的个人密钥。

gpg --list-keys

gpg --gen-key

git config --global user.signingkey 0A46826A!

### 签名标签

如果你已经设置了 GPG 私钥，现在可以使用它来签名新的标签。你只需要使用 -s 而不是 -a 即可。

git tag -s v1.5 -m 'my signed 1.5 tag'

### 验证标签

要验证签名标签，可以使用 git tag -v <tag-name>。此命令使用 GPG 来验证签名。你需要在你的密钥环中拥有签署者的公钥，以便此操作正常工作。

git tag -v v1.4.2.1

### 签名提交

在更新的 Git 版本（v1.7.9 及以上）中，现在也可以签名单个提交。如果你对直接签名提交而不是只签名标签感兴趣，你只需要在 git commit 命令中添加一个 -S 即可。

git commit -a -S -m 'Signed commit'

要查看和验证这些签名，git log 还提供一个 --show-signature 选项。

git log --show-signature -1

此外，你还可以配置 git log 检查它找到的任何签名，并在其输出中使用 %G? 格式列出它们。

git log --pretty="format:%h %G? %aN  %s"

在 Git 1.8.3 及更高版本中，git merge 和 git pull 可以被告知在合并没有携带可信 GPG 签名的提交时进行检查和拒绝，使用 --verify-signatures 命令。

如果你在合并分支时使用此选项，并且它包含未签名且无效的提交，则合并将无法进行。

git merge --verify-signatures non-verify

如果合并只包含有效的签名提交，则合并命令将显示它检查的所有签名，然后继续进行合并。

你也可以在 git merge 命令中使用 -S 选项来对产生的合并提交本身进行签名。以下示例既验证了要合并的分支中的每个提交都已签名，还对产生的合并提交进行了签名。

## 所有人都必须签名

签名标签和提交很棒，但如果你决定在你的正常工作流程中使用它，你需要确保你的团队中的每个人都理解如何操作。可以通过要求每个使用仓库的人运行 git config --local commit.gpgsign true 来实现，以默认自动对他们仓库中的所有提交进行签名。如果你没有这样做，你最终将花费大量时间帮助人们弄清楚如何用签名版本重写他们的提交。在你将此作为你的标准工作流程的一部分之前，请确保你理解 GPG 和签名事物的益处。