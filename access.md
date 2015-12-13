#### 用户权限
`id`可以查看用户相关信息，普通用户的id是从500开始的，每次linux可能不一样
* 用户帐号定义的文件在/etc/passwd下（定义了用户名，uid,gid 真实姓名，主目录以前登录的shell信息）
* 用户组定义的文件在/etc/group下
* 用户密码文件在/etc/shadow下
#### 读取 写入和执行
```bash
    total 32
    -rw-r--r--  1 baozi  staff    36B Dec 13 18:44 README.md
    -rw-r--r--  1 baozi  staff    60B Dec 13 20:46 SUMMARY.md
    drwxr-xr-x  7 baozi  staff   238B Dec 13 20:59 _book
```
* 第一位表示文件类型
* 后9位分别代表，所有者，所属组，其它用户
### Chmod 更改文件模式
注意只有文件的所有者和超级管理员才可以更改文件的权限
#### 八进制表示法来更改权限 8 4 2 1
```bash
7 (rwx) 6 (rw-) 5 (r-x) 4(r--) 0(---)
```
#### 符号表示法
* u user的简写表示文件或者目录的所有者
* g 文件所属群组
* o other的简写
* a all的简写
"+"表示添加权限 "-"表示删除一种权限
"="表示只有指定的权限可以用
```bash
chmod u+x
chmod u-x
chmod +x
chmod u=rwx
chmod go=rw
```
#### umask 设置默认权限
#### su以其他用户和组的id的身份来运行shell
su - 切换到root下
exit 将退出当前环境
#### sudo 以另一个用户的身份执行命令
通过配置普通用户，让用户可以执行管理员的部分命令，而不用输入密码，只需要认证用户的密码
sudo -l 查看授权
#### chown 更改文件所有者和所属群组
```bash
sudo chown baozi filename //把文件所有者从当前所有者更改为用户baozi
sudo chown baozi:_webauthserver test2
```
