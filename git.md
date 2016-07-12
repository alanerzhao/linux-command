
#### git
```
    git config --global //配置全局文件
    git config --list //查看配置信息
    在.git仓库下则配置的是当前仓库的 如果加入--global则配置的全局的
    //默认git是从local 向global查找配置
    git config user.name xxoo
    .gitignore 忽略 文件 
    head是一个一直跟踪你的别名
    它有一个名为 HEAD 的特殊指针。在 Git 中,它是一个指针,指向当前所 在的本地分支(译注:将 HEAD 想象为当前分支的别名)。
    在本例中,你仍然在 master 分支上。因为 git branch 命令仅仅 创建 一个新分支,并不会自动切换到新分支中去
    分支开会会改变你当前工作目录里的文件
    HEAD^ 来查看上一个提交
 HEAD 是当前分支引用的指针,它总是指向该分支上的最后一次提交。这表示 HEAD 将是下一次提交的父结点。 通常,理解 HEAD 的最简方式,就是将它看做 你的上一次提交 的快照   另一种指明祖先提交的方法是 ~。同样是指向第一父提交,因此 HEAD~ 和 HEAD^ 是等价的。
    而区别在于你在后 面加数字的时候。HEAD~2 代表 “第一父提交的第一父提交”,也就是 “祖父提交” —— Git 会根据你指定的次 数获取对应的第一父提交。例
    如,在之前的列出的提交历史中,HEAD~3 就是
    提交区间
    拉取远程分支并不会在本地新建一个分支，但你可以关联远程分支
    git checkout -b serverfix origin/serverfix
    删除远程 分支
    git push origin --deletel serverfix
    变基
    rebase命令将提交到某一分支上的所有修改都移至另一分支上
    git checkout experiment 
    git rebase master
    test
    git rm --cached README删除暂存区
```
#### git rebase -i 
```
    git rebase 可以对历史记录重写
    把你需要重写的记录告诉它
    git rebase -i HEAD~3
    操作完成
    git commit --amaend则会循序执行修改
    git rebase --continue 则执行完成
    可以较强的学习一下
    git rebase -i HEAD~3 删除一个再保存，则可以删除历史信息
    git rm xxoo.txt
    合并历史用squaned
    核武器级选项:filter-branch(略)
```
HEAD 上一次提交的快照,下一次提交的父结点
Index 预期的下一次提交的快照
Working Directory 沙盒

HEAD 是当前分支引用的指针,它总是指向该分支上的最后一次提交。这表示 HEAD 将是下一次提交的父结点。
通常,理解 HEAD 的最简方式,就是将它看做 你的上一次提交 的快照。

索引是你的 预期的下一次提交。我们也会将这个概念引用为 Git 的 “暂存区域”,这就是当你运行 git
commit 时 Git 看起来的样子。

最后,你就有了自己的工作目录。另外两棵树以一种高效但并不直观的方式,将它们的内容存储在 .git 文件夹 中。工作目录会将它们解包为实际的文件以便编辑。你可以把工作目录当做 沙盒。在你将修改提交到暂存区并 记录到历史之前,可以随意更改。
