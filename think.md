##### 关于可执行命令为什么能执行？
当我ls后，shell不会查找整个计算机系统，来找/bin/ls而是查找一个目录列表，这些目录包含在PATH变量中
PATH变量经常在/etc/profile启动文件中设置
比如
export PATH="$PATH:$HOME/bin" # Add RVM to PATH for scripting
这里记住一定要追加否则导致所有执行的变量找不到
这样你在你家目录的bin下面随便写可执行程序都不用在当前目录执行
在全局环境下也可以找的到

##### shell环境

shell在环境中存储了两种基本类型的数据，环境变量和shell变量

```bash
    printenv 打印所有的环境变量
    set 设置shell选项(显示所有shell和环境变量)
    export 导出环境变量，让随后执行的程序知道
    alias 创建命令别名
```

`PATH` 环境变量是由冒号分开的目录列表，当你输入可执行程序名后，会搜索这个目录列表

```bash
    /etc/bash.bashrc 应用于所有用户 全局配置文件
    /etc/profile 应用于所有用户的全局配置
    ~/.bash_profile 用户私人的启动文件。可以用来扩展或重写全局配置
    ~/.bash_login 如果上面文件没有找到，bash会尝试读取这个脚本
    ~/.profile 如果文件~/.bash_profile 都没有找到，bash会试图读取这个文件
    ~/.bashrc 用户私有的启动文件。可以用来扩展或重写全局配置脚本
```
看一下profile中就对nvm做了配置，启动的时候写入环境变量




