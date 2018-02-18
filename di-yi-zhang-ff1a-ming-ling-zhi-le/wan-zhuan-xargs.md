xargs 命令把从 stdin 接收到的数据重新格式化，再将其作为参数提供给其他命令。

xargs 可以作为一种替代，其作用类似于 find 命令中的  -exec 。下面是各种 xargs 命令的使用技巧。

\(1\) 将多行输入转换成单行输出。

只需要将换行符移除，再用 " " （空格）进行代替，就可以实现多行输入的转换。 '\n'被解释成一个换行符，换行符其实就是多行文本之间的定界符。利用 xargs ，我们可以用 空格替换掉换行符，这样就能够将多行文本转换成单行文本：

```
$ cat example.txt #  样例文件
1 2 3 4 5 6
7 8 9 10
11 12

$ cat example.txt | xargs
1 2 3 4 5 6 7 8 9 10 11 12
```

\(2\)将单行输入转换成多行输出。

```
$ cat example.txt | xargs -n 3
1 2 3
4 5 6
7 8 9
10 11 12
```

\(3\)可以用自己的定界符来分隔参数。用 -d 选项为输入指定一个定制的定界符：

```
$ echo "splitXsplitXsplitXsplit" | xargs -d X
split split split split
```

结合 -n 选项，我们可以将输入划分成多行，而每行包含两个参数：

```
$ echo "splitXsplitXsplitXsplit" | xargs -d X -n 2
split split
split split
```

\(4\) 结合 find 使用 xargs

xargs 和 find 算是一对死党。两者结合使用可以让任务变得更轻松。

用 find 匹配并列出所有的 .txt文件，然后用 xargs 将这些文件删除：

```
$ find /home/myshell/ -name "*.txt" | xargs rm -f
```

但这样做很危险。有时可能会删除不必要删除的文件。我们没法预测分隔 find 命令输出结果的定界符究竟是什么（ '\n' 或者 ' ' ） 。很多文件名中都可能会包含空格符（ ' ' ） 因此 xargs 很可能会误认为它们是定界符（例如，hell text.txt会被 xargs 误解为hell和text.txt） 。 只要我们把 find 的输出作为 xargs 的输入， 就必须将  -print0 与 find 结合使用， 以字符null （ '\0' ）来分隔输出。

```
$ find /home/myshell/ -name "*.txt" -print0 | xargs -0 rm -f
```

\(5\) 统计 /home/myshell 目录中sh文件的行数：

```py
$ find /home/myshell/ -type f -name "*.sh" -print0 | xargs -0 wc -l

 18 /home/myshell/sleep.sh
   5 /home/myshell/variables.sh
   9 /home/myshell/time_take.sh
  10 /home/myshell/printf.sh
   7 /home/myshell/pwd.sh
   7 /home/myshell/isroot.sh
   6 /home/myshell/log.sh
  62 total
```



