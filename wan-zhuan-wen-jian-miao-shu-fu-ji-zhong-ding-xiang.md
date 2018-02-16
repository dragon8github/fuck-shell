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

5、还可以利用下面这个更好的方法将 stderr 转换成 stdout ，使得 stderr 和 stdout  
 都被重定向到同一个文件中：

```py
$ fuckyou &> stdin.txt

$ cat stderr.txt
-bash: fuckyou: command not found
```

6、如果你仅仅想要屏蔽错误，不想产生输出文件，那么你可以重定向到/dev/null中，此处被称为Unix中的黑洞

```
$ fuckyou &> /dev/null
```

7、如果对 stderr 或 stdout 进行重定向，被重定向的文本会传入文件。因为文本  
已经被重定向到文件中， 也就没剩下什么东西可以通过管道 （ \| ） 传给接下来的命令。

```py
$ echo 123 1>stdin.txt | cat -n # 管道返回为空，所以cat命令不执行。
$ cat std
```

但是有一个方法既可以将数据重定向到文件，还可以提供一份重定向数据的副本作为后续命令的 stdin 。这可以使用 tee 来实现。

```py
$  printf "123\n123\n123\n" | tee stdin. | cat -n

1  123
2  123
3  123
```

**tee 只能对stdin（标准输出）起作用。**

