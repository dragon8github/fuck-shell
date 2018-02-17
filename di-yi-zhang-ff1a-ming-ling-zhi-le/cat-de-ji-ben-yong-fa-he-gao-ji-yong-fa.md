cat 是命令行玩家首先必须学习的命令之一。

#### 1.打印单个文件的内容：

```
$ cat file.txt
```

This is a line inside file.txt

This is the second line inside file.txt

#### 2.打印多个文件的内容：

```
$ cat one.txt two.txt
```

This is line from one.txt

This is line from two.txt

#### 3.摆脱多余的空白行

有时候文本文件中可能包含多处连续的空白行。如果你需要删除这些额外的空白行，使用下  
面的方法：

#### 4.将制表符显示为 ^\|

单 从视觉上很难将制表符同连续的空格区分开。而在用Python编写程序时，用于代码缩进的 制表符以及空格是具有特殊含义的。因此，若在应该使用空格的地方误用了制表符的话，就会产 生缩进错误。仅仅在文本编辑器中进行观察是很难发现这种错误的。 cat 有一个特性，可以将制 表符着重标记出来。该特性对排除缩进错误非常有用。用 cat 命令的 -T 选项能够将制表符标记成 ^\| 。例如：

```py
$ cat file.py
def function():
    var = 5
    next = 6
    third = 7

$ cat -T file.py
def function():
^Ivar = 5
^Inext = 6
^Ithird = 7
```

#### 5.行号

```
$ cat lines.txt
line
line
line

$ cat -n lines.txt
1 line
2 line
3 line
```

**-n 甚至会为空白行加上行号。如果你想跳过空白行，那么可以使用选项 -b 。**



