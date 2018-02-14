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

