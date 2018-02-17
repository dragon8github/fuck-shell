在日常工作中使用shell时，有时候命令只有满足某些条件或是某种外部事件（例如文件可以被下载）操作才能够成功执行。这种情况下，你可能希望重复执行命令，直到成功为止。

可以把它放入~/.bashrc文件，更便于使用：

```py
repeat()
{
    while true
    do
        $@ && return
    done
}

repeat() { while true; do $@ && return; done }
```

#### 一种更快的做法

在大多数现代系统中， true 是作为/bin中的一个二进制文件来实现的。这就意味着每执行一次 while 循环，shell就不得不生成一个进程。如果不想这样，可以使用shell内建的“ : ”命令，它总是会返回为0的退出码：

```
repeat() { while :; do $@ && return; done }
```

尽管可读性不高，但是肯定比第一种方法快。

