# git 命令

## 1、git基本命令

1）git add 将想要快照的内容写入缓存区
2）git status -s "AM" 状态的意思是，这个文件在我们将它添加到缓存之后又有改动
3）git commit -m '第一次版本提交' -m选项添加备注信息
4）git clone url 使用 git clone 拷贝一个 Git 仓库到本地
5）git diff 查看执行 git status 的结果的详细信息
　　尚未缓存的改动：git diff
　　查看已缓存的改动： git diff --cached
　　查看已缓存的与未缓存的所有改动：git diff HEAD
　　显示摘要而非整个 diff：git diff --stat
6）git commit -a 跳过git add 提交缓存的流程 
7）git reset HEAD 用于取消已缓存的内容
8）git rm file 
　　git rm 会将条目从缓存区中移除。这与 git reset HEAD 将条目取消缓存是有区别的。
　　"取消缓存"的意思就是将缓存区恢复为我们做出修改之前的样子。
　　默认情况下，git rm file 会将文件从缓存区和你的硬盘中（工作目录）删除。
9）git mv 重命名磁盘上的文件 如 git mv README README.md

10）git push -u origin master 提交代码

## 2、git 分支管理

1）创建分支命令 git branch (branchname) 列出分支 git branch
2）切换分支命令 git checkout (branchname)
3）合并分支 git merge (branchname)
4）创建新分支并立即切换到该分支下 git checkout -b (branchname)
5）删除分支命令 git branch -d (branchname)
ps:状态 uu 表示冲突未解决 可以用 git add 要告诉 Git 文件冲突已经解决

## 3、查看日志版本

git log 命令列出历史提交记录
git log --oneline 查看历史记录的简洁的版本
git log --oneline --graph 查看历史中什么时候出现了分支、合并

## 4、标签

为软件发布创建标签是推荐的。这个概念早已存在，在 SVN 中也有。你可以执行如下命令创建一个叫做 1.0.0 的标签：
git tag 1.0.0 1b2e1d63ff
1b2e1d63ff 是你想要标记的提交 ID 的前 10 位字符。可以使用下列命令获取提交 ID：
git log
你也可以使用少一点的提交 ID 前几位，只要它的指向具有唯一性

## 5、提取远程仓库代码

1）git fetch　　从远程仓库下载新分支与数据

2)）git pull　　从远端仓库提取数据并尝试合并到当前分支

## 注意

更改分支后需要初始化 git push -u origin master

