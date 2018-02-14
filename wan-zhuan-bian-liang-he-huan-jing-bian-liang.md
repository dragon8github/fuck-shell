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



