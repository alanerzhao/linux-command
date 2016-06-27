#### 概述

使用 tmux，你可以创造一个如图1（使用 tmux 作为开发环境）所示的工作环境。使用 tmux 的窗口，你可以非常轻松地在一个非常简单的环境中管理文本编辑器、数据库控制台、本地 web 服务器。你还可以把 tmux 窗口分割为多个区域，让多个程序并排显示或运行。这意味着你可以在一个窗口里让文本浏览器，irc 聊天客户端，或自动化测试与你的主编辑器同时显示、运行。

最棒的是，你仅仅通过键盘快捷键就可以非常快速地在这些窗口和面板之间互相移动，这样会极大地提高你的注意力和生产效率。

在这本书中，你可以学到如何配置、使用并自定义 tmux。你会学习到如何同时管理多个程序，编写脚本来创建自定义的环境，还能学会如何使用 tmux 与其他人远程工作。使用 tmux，你可以创建一个几乎纯键盘操作的工作环境。

tmux 是一个终端复用器（terminal multiplexer）。它让我们可以使用单一环境就可以登录多个终端或窗口，每个终端或窗口都运行着独立的进程或程序。例如，我们可以打开 tmux 然后运行 Vim 编辑器。然后可以新建一个窗口运行一个数据库控制台，然后在这些程序之间来回切换，这一切都是在一个会话（session）中进行的。

如果你使用了一个现代操作系统并且终端有标签页功能的话，这听起来并不新鲜。但是同时运行多个程序只是 tmux 的特性之一。我们可以将窗口（window）划分为水平或垂直面板（pane），也就是说可以在同一个屏幕上并排显示或运行两个或多个程序。这些操作都不使用鼠标。

我们还能从一个会话中分离出来，让整个工作环境都在后台运行。如果你以前用过 GNU-Screen，那你对这个特性一定感到很熟悉。tmux 与 GNU-Screen 有许多的相似之处，但是 tmux 的功能更多，而且 tmux 的配置更容易。由于 tmux 使用了 client-server 模型，因此可以在一个中央位置控制窗口和面板，甚至可以从一个终端窗口就实现多个会话之间的切换。这个 client-server 模型还可以让我们创建 tmux 脚本并与其他窗口或应用程序交互。
#### tmux 退出
```bash
eixt
```

#### 创建命名会话

```bash
tmux -s new-session name
tmux new -s name
ctrl -b  d (分离会放)
tmux list-sessions 列出所有会话
tmux ls  简写
tmux attach 连接会话
如果存在多个会话需要要切出来再attatch
tmux attach - t name 打开指定的会话
tmux attact -t name -d 在后台运行
tmux kill-session -t basic 杀死会话
tmux kill-session 杀死所有client server
```
#### 使用窗口

```bash
tmux new -s windows -n shell (-n 可以命名) windows 窗口下的shell窗口
ctrl -b c （创建新人窗口）
ctrl -b , 重命名窗口名称
ctrl -b n , p 窗口切换或者ctrl -b 0-9
超过9个那么就按ctrl -b f(find)
ctrl -b w 查看有多少窗口
ctrl -b s 查看有多少会话
ctrl -b & 关闭窗口
```

#### 使用面板

```bash
ctrl -b % 切成面板
ctrl -b " 水平切分
ctrl -b o 切换面板
ctrl -b  方向键
ctrl -b spance 切换布局风格
ctrl -b X 退出  或者 exit

```
#### 命令模式

```bash
ctrl -b : 进入命令模式
new-window -n console 命名为console
new-window -n processes "top"
ctrl-b ?
```
以备查阅

创建会话

命令	描述
tmux new-session	创建一个未命名的会话。可以简写为 tmux new 或者就一个简单的 tmux
tmux new -s development	创建一个名为 development 的会话
tmux new -s development -n editor	创建一个名为 development 的会话并把该会话的第一个窗口命名为 editor
tmux attach -t development	连接到一个名为 development 的会话
会话、窗口和面板的默认快捷键

快捷键	功能
PREFIX d	从一个会话中分离，让该会话在后台运行。
PREFIX :	进入命令模式
PREFIX c	在当前 tmux 会话创建一个新的窗口，是 new-window 命令的简写
PREFIX 0...9	根据窗口的编号选择窗口
PREFIX w	显示当前会话中所有窗口的可选择列表
PREFIX ,	显示一个提示符来重命名一个窗口
PREFIX &	杀死当前窗口，带有确认提示
PREFIX %	把当前窗口垂直地一分为二，分割后的两个面板各占 50% 大小
PREFIX "	把当前窗口水平地一分为二，分割后的两个面板各占 50% 大小
PREFIX o	在已打开的面板之间循环移动当前焦点
PREFIX q	短暂地显示每个面板的编号
PREFIX x	关闭当前面板，带有确认提示
PREFIX SPACE	循环地使用 tmux 的几个默认面板布局
