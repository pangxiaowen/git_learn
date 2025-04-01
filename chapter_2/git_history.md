## 查看提交历史

默认情况下，在没有参数的情况下，git log 会按反时间顺序列出在该仓库中进行的提交

git log

选项 -p 或 --patch，它会显示每个提交中引入的差异（补丁输出）。 -2 只显示最后两个条目。

git log -p -2

查看每个提交的一些简要统计信息，可以使用 --stat 选项

git log --stat

另一个非常有用的选项是 --pretty。此选项将日志输出更改为默认值以外的其他格式。

git log --pretty=oneline

git log --pretty=format:"%h - %an, %ar : %s"

https://git-scm.cn/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format

--graph 此选项添加了一个漂亮的 ASCII 图表，显示你的分支和合并历史记录。

git log --pretty=format:"%h %s" --graph

## 限制日志输出

你可以使用 -<n>，其中 n 是任何整数，以显示最后 n 个提交。

git log -2

诸如 --since 和 --until 之类的时间限制选项非常有用。例如，此命令获取过去两周内进行的提交列表。

git log --since=2.weeks

此命令支持多种格式——你可以指定特定日期，例如 "2008-01-15"，或相对日期，例如 "2 years 1 day 3 minutes ago"。

你还可以将列表过滤到与某些搜索条件匹配的提交。--author 选项允许你根据特定作者进行过滤，而 --grep 选项允许你在提交消息中搜索关键字。

另一个非常有用的过滤器是 -S 选项（俗称 Git 的“镐”选项），它接受一个字符串，并且只显示更改该字符串出现次数的那些提交
例如，如果你想查找最后添加或删除对特定函数的引用的提交，你可以调用

git log -S printf

传递给 git log 作为过滤器的最后一个真正有用的选项是路径

git log -- chapter_2/main.cpp

| 选项   |	描述 |
| ---   |  --- |
|-<n>   | 仅显示最后 n 个提交。|
|--since, --after | 将提交限制为在指定日期之后进行的提交。|
| -until, --before| 将提交限制为在指定日期之前进行的提交。|
| --author | 仅显示作者条目与指定字符串匹配的提交。|
| --committer | 仅显示提交者条目与指定字符串匹配的提交。|
| --grep | 仅显示提交消息包含该字符串的提交。|
| -S	| 仅显示添加或删除与该字符串匹配的代码的提交。|