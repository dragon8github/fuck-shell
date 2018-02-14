### 获得与该进程相关的环境变量：

```
$ cat /proc/<PID>/environ
```

Example：假设我们有一个名为gedit的应用程序正在运行

```
$ pgrep gedit
12501

$ cat /proc/12501/environ
GDM_KEYBOARD_LAYOUT=usGNOME_KEYRING_PID=1560USER=slynuxHOME=/home/slynux
```

环境变量远不止这些， 只是由于对页面篇幅的限制， 在这里删除了其他很多环境变量。

变量以 name=value 的形式来描述，彼此之间由null字符（ \0 ）分隔。如果你将 \0 替换成 \n ，那么就可以将输出重新格式化，使得每一行显示一组“变量=值” 。替换可以使用`tr`命令来实现：

```
$ cat /proc/12501/environ | tr '\0' '\n'
```

![](/assets/import.pngasasasd)

### 变量的赋值

```
$ test="hello world"
$ echo $test
hello world
```

Example：我们可以在 printf 或 echo 命令的双引号中引用变量值。

```
#!/bin/bash
# 文件名:variables.sh
fruit=apple
count=5
echo "We have $count ${fruit}"
```

输出如下：We have 5 apple

### 用 export 命令来设置环境变量

在默认情况下，有很多标准环境变量可供shell继承使用。

PATH 就是其中之一。通常，变量 PATH 包含：

```
$ echo $PATH
/usr/local/jdk-9.0.4/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
```

PATH 通常定义在/etc/environment或/etc/profile或~/.bashrc中。

如果需要在 PATH 中添加一条新路径，可以使用：

```
$ export PATH="$PATH:/home/user/bin"
```

也可以使用

```
$ PATH="$PATH:/home/user/bin"
$ export PATH

$ echo $PATH
/home/slynux/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr
/games:/home/user/bin
```

这样，我们就将/home/user/bin添加到了 PATH 中。

### 获得字符串长度

```
$ length=${#var}
```

Example

```
$ var=12345678901234567890
echo ${#var}
20
```

### 识别当前所使用的shell

```
$ echo $SHELL
/bin/bash

$ echo $0
/bin/bash
```

### 检查是否为超级用户

UID 是一个重要的环境变量，可以用于检查当前脚本是以超级用户还是以普通用户的身份运行的。

```
$ echo $UID
0
```

Example

```bash
#!/bin/bash
#文件名: isroot.sh
if [ $UID -ne 0 ]; then
    echo Non root user. Please run as root.
else
    echo Root user
fi
```

运行结果：Root user

