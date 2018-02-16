在编写脚本的时候会频繁使用标准输入（ stdin ） 、标准输出（ stdout ）和标准错误（ stderr ） 。

通过内容过滤将输出重定向到文件是我们平日里的基本任务之一。

* 0 ——  stdin （标准输入）
* 1 ——  stdout （标准输出）
* 2 ——  stderr （标准错误）

1、将输出文本重定向或保存到一个文件中：

```
$ echo "This is a sample text 1" > temp.txt
```

2、将文本追加到目标文件中，看下面的例子：

```
$ echo "This is a sample text 2" >> temp.txt
```

3、来看看什么是 stderr \(标准错误\) 以及如何对它重定向：

```
$ ls +
ls: cannot access +: No such file or directory

$ ls + 2> out.txt # 正常运行
$ cat ./out.txt
ls: cannot access +: No such file or directory
```

当命令成功完成后，退出状态可以从特殊变量 $?中获得 （在命令执行之后立刻运行 echo $? ， 就可以打印出退出状态）

```
$ echo $?
```

坑爹： 请注意 \`\` 代码块中报错的情况，来看看下面的例子：

    $ echo `123`
    -bash: 123: command not found

    $ echo `123` 2>stderr.txt # 无法阻止报错
    -bash: 123: command not found
    $ cat stderr.txt # 日志为空

原因是 \`\` 为一个单独的执行块，所以外部无法捕捉。需要单独在 ·· 中捕捉：

    $ echo `123 2>stderr.txt` # 没有报错，由于``代码块中报错，返回值为空，所以外部输出一段空字符串

    $ cat stderr.txt # 日志正常记录
    -bash: 123: command not found

4、你可以将 stderr 单独重定向到一个文件，将 stdout 重定向到另一个文件：

```
$ fuckyou 2>stderr.txt 1>stdout.txt  # 系统没有fuckyou这个命令

$ cat stderr.txt
-bash: fuckyou: command not found
```

5、还可以利用下面这个更好的方法将 stderr 转换成 stdout ，使得 stderr 和 stdout 都被重定向到同一个文件中：

```
$ fuckyou &> stdin.txt

$ cat stderr.txt
-bash: fuckyou: command not found
```



