### 根据扩展名切分文件名

有一些脚本是依据文件名进行各种处理的。我们可能会需要在保留扩展名的同时修改文件名、转换文件格式或提取部分文件名。shell所具有的一些内建 功能可以依据不同的情况来切分文件名。

#### 1.借助%操作符可以轻松将名称部分从“名称.扩展名”这种格式中提取出来。

你可以按照下面 的方法从sample.jpg中提取名称。

```
file_jpg="sample.jpg"
name=${file_jpg%.*}
echo File name is: $name
```

输出结果：File name is: sample

#### 2.下一个任务是将文件名的扩展名部分提取出来，这可以借助 \# 操作符实现。

```
$ extension=${file_jpg#*.}
$ echo Extension is: jpg
```

输出结果： Extension is: jpg

### ${VAR%.\*} 的含义如下所述：

* 从 $VAR中删除位于 % 右侧的通配符（在前例中是.\*）所匹配的字符串。通配符从右向左 进行匹配。
* 给VAR赋值，VAR=sample.jpg。那么，通配符从右向左就会匹配到.jpg，因此，从 $VAR 中删除匹配结果，就会得到输出sample。

%属于贪婪（greedy）操作。它会从右到左匹配符合条件的最长的字符串。

%%属于非贪婪（non-greedy）操作。它从右到左找出匹配通配符的最短结果。

```
$ VAR=hack.fun.book.txt
$ echo ${VAR%.*} 
hack.fun.book

$ echo ${VAR%%.*}
hack
```

###  ${VAR\#\*.}的含义如下所述：

 从$VAR中删除位于\#右侧的通配符（即在前例中使用的\*.）所匹配的字符串。通配 符从左向右进行匹配。

```
$ VAR=hack.fun.book.txt
$ echo ${VAR#*.}
fun.book.txt

$ echo ${VAR##*.}
txt
```



