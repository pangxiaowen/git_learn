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