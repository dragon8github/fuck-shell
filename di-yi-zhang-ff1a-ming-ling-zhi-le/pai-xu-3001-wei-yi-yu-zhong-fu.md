### 排序、唯一与重复

同文本文件打交道时，少不了要用到排序。sort命令能够帮助我们对文本文件和stdin进行 排序操作。它通常会配合其他命令来生成所需要的输出。uniq是一个经常与sort一同使用的命 令。它的作用是从文本或stdin中提取唯一（或重复）的行。

#### \(1\) 我们可以按照下面的方式轻松地对一组文件（例如file1.txt和file2.txt）进行排序：

```py
$ sort file1.txt file2.txt > sorted.txt

# 或是

$ sort file1.txt file2.txt -o sorted.txt
```

#### \(2\) 按照数字顺序进行排序（由小到大）：

```
$ sort -n file.txt
```

#### \(3\) 按照逆序进行排序（由大到小）：

```
$ sort -r file.txt
```

#### \(4\) 按照月份进行排序（依照一月，二月，三月……）：

```
$ sort -M months.txt
```

#### \(5\) 合并两个已排序过的文件：

```
$ sort -m file.txt file2.txt
```

#### \(6\) 找出已排序文件中不重复的行：

```
$ sort file1.txt file2.txt | uniq
```

#### \(7\) 检查文件是否已经排序过：

```py
#!/bin/bash
# 功能描述：排序
sort -C filename ;
if [ $? -eq 0 ]; then
 echo Sorted;
else
 echo Unsorted;
fi
```

将filename替换成你需要进行检查的文件名，然后运行该脚本。

## uniq

uniq命令通过消除重复内容，从给定输入中（stdin或命令行参数文件）找出唯一的行。它也可以用来找出输入中出现的重复行。 

uniq只能作用于排过序的数据输入，因此，uniq要么使用管道，要么将排过序的文件作为输入，与sort命令结合使用。

\(1\)  从给定的输入数据中生成唯一的行：

```py
$ cat sorted.txt
bash
foss
hack
hack

$ uniq sorted.txt
bash
foss
hack 

# 或是
$ sort unsorted.txt | uniq
```

\(2\) 只显示唯一的行，排除有重复出现的行：

```py
$ uniq -u sorted.txt
bash
foss
```



