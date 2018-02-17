我们通常使用管道并利用子shell的方式将多个文件的输出组合起来。

\(1\) 先从组合两个命令开始：

```
$ ls | cat -n > out.txt
```

\(2\) 子shell / 反引用 / 反标记

    cmd_output=`ls | cat -n`
    echo $cmd_output

    cmd_output=$(ls | cat -n)
    echo $cmd_output



