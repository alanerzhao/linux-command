
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
    分支开会会改变你当前工作目录里的文件
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

```
子模块
```
git submodule add  url
cd submoduledir git submodule init
git submodule update
git clone命令传递--recursive选项,它就会自动初始化并更新仓库 中的每一个子模块。
//如果你不想在子目录中手动抓取与合并,那么还有种更容易的方式。
git submodule update --remote,Git 将会进入子模块然后抓取并更新。
```
在包含子模块的项目上工作 现在我们有一份包含子模块的项目副本,我们将会同时在主项目和子模块项目上与队员协作。
拉取上游修改
在项目中使用子模块的最简模型,就是只使用子项目并不时地获取更新,而并不在你的检出中进行任何更改。我
们来看一个简单的例子。
如果想要在子模块中查看新工作,可以进入到目录中运行git fetch与git merge,合并上游分支来更新本 地代码。

你很有可能正在使用子模块,因为你确实想在子模块中编写代码的同时,还想在主项目上编写代码(或者跨子模 块工作)。否则你大概只能用简单的依赖管理系统(如 Maven 或 Rubygems)来替代了。
现在我们将通过一个例子来演示如何在子模块与主项目中同时做修改,以及如何同时提交与发布那些修改。
到目前为止,当我们运行git submodule update从子模块仓库中抓取修改时,Git将会获得这些改动并更新 子目录中的文件,但是会将子仓库留在一个称作 “游离的 HEAD” 的状态。这意味着没有本地工作分支(例如 “master”)跟踪改动。所以你做的任何改动都不会被跟踪。
为了将子模块设置得更容易进入并修改,你需要做两件事。首先,进入每个子模块并检出其相应的工作分支。接 着,若你做了更改就需要告诉Git它该做什么,然后运行git submodule update --remote来从上游拉取 新工作。你可以选择将它们合并到你的本地工作中,也可以尝试将你的工作变基到新的更改上。
首先,让我们进入子模块目录然后检出一个分支。

为了确保这不会发生,你可以让Git在推送到主项目前检查所有子模块是否已推送。git push命令接受可以设 置为 “check” 或 “on-demand” 的 --recurse-submodules 参数。如果任何提交的子模块改动没有推送 那么 “check” 选项会直接使 push 操作失败。
on-demand

子模块遍历
有一个 foreach 子模块命令,它能在每一个子模块中运行任意命令。如果项目中包含了大量子模块,这会非常 有用。
例如,假设我们想要开始开发一项新功能或者修复一些错误,并且需要在几个子模块内工作。我们可以轻松地保
存所有子模块的工作进度。

git submodule foreach 'git checkout -b featureA'
  Entering 'CryptoLibrary'
  Switched to a new branch 'featureA'
  Entering 'DbConnector'
  Switched to a new branch 'featureA'

git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
  $ git config alias.spush 'push --recurse-submodules=on-demand'
  $ git config alias.supdate 'submodule update --remote --merge'
 
这样当你想要更新子模块时可以简单地运行git supdate,或git spush检查子模块依赖后推送。
移除那个目录并不困难,但是有一个目录在那儿会让人有一点困惑。如果你移除它然后切换回有那个子模块的分 支,需要运行submodule update --init来重新建立和填充。

commit.template
如果把此项指定为你的系统上某个文件的路径,当你提交的时候, Git 会使用该文件的内容作为提交的默认信 息。例如:假设你创建了一个叫 ~/.gitmessage.txt 的模板文件,类似这样:
  subject line
  what happened
  [ticket: X]
要想让 Git 把它作为运行 git commit 时显示在你的编辑器中的默认信息, 如下设置 commit.template: $ git config --global commit.template ~/.gitmessage.txt
$ git commit
然后当你提交时,编辑器中就会显示如下的提交信息占位符:


core.excludesfile
正如 忽略文件 所述,你可以在你的项目的 .gitignore 文件里面规定无需纳入 Git 管理的文件的模板,这样它
们既不会出现在未跟踪列表,也不会在你运行git add后被暂存。 不过有些时候,你想要在你所有的版本库中忽略掉某一类文件。如果你的操作系统是 OS X,很可能就是指
.DS_Store。如果你把 Emacs 或 Vim 作为首选的编辑器,你肯定知道以 ~ 结尾的临时文件。 这个配置允许你设置类似于全局生效的 .gitignore 文件。如果你按照下面的内容创建一个
~/.gitignore_global 文件: *~
.DS_Store
......然后运行git config --global core.excludesfile ~/.gitignore_global,Git将把那些文件 永远地拒之门外。



格式化与多余的空白字符
格式化与多余的空白字符是许多开发人员在协作时,特别是在跨平台情况下,不时会遇到的令人头疼的琐碎的问 题。由于编辑器的不同或者文件行尾的换行符在 Windows 下被替换了,一些细微的空格变化会不经意地混入提 交的补丁或其它协作成果中。不用怕,Git 提供了一些配置项来帮助你解决这些问题。
core.autocrlf
假如你正在 Windows 上写程序,而你的同伴用的是其他系统(或相反),你可能会遇到 CRLF 问题。这是因为 Windows 使用回车(CR)和换行(LF)两个字符来结束一行,而 Mac 和 Linux 只使用换行(LF)一个字符。 虽然这是小问题,但它会极大地扰乱跨平台协作。许多 Windows 上的编辑器会悄悄把行尾的换行字符转换成回 车和换行,或在用户按下 Enter 键时,插入回车和换行两个字符。
Git 可以在你提交时自动地把回车和换行转换成换行,而在检出代码时把换行转换成回车和换行。你可以用 core.autocrlf 来打开此项功能。如果是在 Windows 系统上,把它设置成 true,这样在检出代码时,换行 会被转换成回车和换行:
  $ git config --global core.autocrlf true
如果使用以换行作为行结束符的 Linux 或 Mac,你不需要 Git 在检出文件时进行自动的转换;然而当一个以回车 加换行作为行结束符的文件不小心被引入时,你肯定想让 Git 修正。你可以把 core.autocrlf 设置成 input 来 告诉 Git 在提交时把回车和换行转换成换行,检出时不转换:
  $ git config --global core.autocrlf input
这样在 Windows 上的检出文件中会保留回车和换行,而在 Mac 和 Linux 上,以及版本库中会保留换行。
如果你是 Windows 程序员,且正在开发仅运行在 Windows 上的项目,可以设置 false 取消此功能,把回车保 留在版本库中:
  $ git config --global core.autocrlf false
core.whitespace
Git 预先设置了一些选项来探测和修正多余空白字符问题。它提供了六种处理多余空白字符的主要选项 —— 其中 三个默认开启,另外三个默认关闭,不过你可以自由地设置它们。
默认被打开的三个选项是:blank-at-eol,查找行尾的空格;blank-at-eof,盯住文件底部的空 行;space-before-tab,警惕行头 tab 前面的空格。
默认被关闭的三个选项是:indent-with-non-tab,揪出以空格而非 tab 开头的行(你可以用 tabwidth 选 项控制它);tab-in-indent,监视在行头表示缩进的 tab;cr-at-eol,告诉 Git 忽略行尾的回车。
   
通过设置 core.whitespace,你可以让 Git 按照你的意图来打开或关闭以逗号分割的选项。要想关闭某个选项,你可以在输入设置选项时不指定它或在它前 面加个 -。例如,如果你想要打开除 cr-at-eol 之外的所有选项:
  $ git config --global core.whitespace \
      trailing-space,space-before-tab,indent-with-non-tab
当你运行git diff命令并尝试给输出着色时,Git将探测到这些问题,因此你在提交前就能修复它们。用git apply 打补丁时你也会从中受益。如果正准备应用的补丁存有特定的空白问题,你可以让 Git 在应用补丁时发出 警告:
  $ git apply --whitespace=warn <patch>
或者让 Git 在打上补丁前自动修正此问题:
  $ git apply --whitespace=fix <patch>
这些选项也能运用于git rebase。如果提交了有空白问题的文件,但还没推送到上游,你可以运行git rebase --whitespace=fix来让Git在重写补丁时自动修正它们。


Git 属性
你也可以针对特定的路径配置某些设置项,这样 Git 就只对特定的子目录或子文件集运用它们。这些基于路径的 设置项被称为 Git 属性,可以在你的目录下的 .gitattributes 文件内进行设置(通常是你的项目的根目 录)。如果不想让这些属性文件与其它文件一同提交,你也可以在 .git/info/attributes 文件中进行设 置。
通过使用属性,你可以对项目中的文件或目录单独定义不同的合并策略,让 Git 知道怎样比较非文本文件,或者 让 Git 在提交或检出前过滤内容。在本节,你将学习到一些能在自己的项目中用到的属性,并看到几个实际的例 子。

Git 钩子
和其它版本控制系统一样,Git 能在特定的重要动作发生时触发自定义脚本。有两组这样的钩子:客户端的和服 务器端的。客户端钩子由诸如提交和合并这样的操作所调用,而服务器端钩子作用于诸如接收被推送的提交这样 的联网操作。你可以随心所欲地运用这些钩子。

