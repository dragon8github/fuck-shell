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



