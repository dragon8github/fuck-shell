comm命令可用于两个文件之间的比较。它有很多不错的选项可用来调整输出，以便我们执 行交集、求差（difference）以及差集操作：

* 交集：打印出两个文件所共有的行。
* 求差：打印出指定文件所包含的且互不相同的那些行。
* 差集：打印出包含在文件A中，但不包含在其他指定文件中的那些行。

```
$ cat A.txt
apple
orange
gold
silver
steel
iron

$ cat B.txt
orange
gold
cookies
carrot
```

#### 需要注意的是comm必须使用排过序的文件作为输入。

```
$ sort A.txt -o A.txt ; sort B.txt -o B.txt
```

#### \(1\) 首先执行不带任何选项的comm：

```
$ comm A.txt B.txt 

apple
        carrot
        cookies
                gold
iron
                orange
silver
steel
```

输出的第一列包含只在A.txt中出现的行，第二列包含只在B.txt中出现的行，第三列 包含A.txt和B.txt中相同的行。各列以制表符（\t）作为定界符。

#### \(2\) 为了打印两个文件的交集，我们需要删除第一列和第二列，只打印出第三列：

```
$ comm A.txt B.txt -1 -2
gold
orange
```

#### \(3\) 打印出两个文件中不相同的行：

```
$ comm A.txt B.txt -3

apple
        carrot
        cookies
iron
silver
steel
```

#### \(4\) 要生成规范的输出，得使用下面的命令：

```
$ comm A.txt B.txt -3 | sed 's/^\t//' 

apple
carrot    
cookies
iron
silver
steel
```

在生成统一输出时，sed命令通过管道获取comm的输出。它删除行首的 \t字符。sed中的s 表示替换（substitute）。/^\t/ 匹配行前的 \t（^是行首标记）。//（两个/操作符之间没有任何 字符）是用来替换行首的\t的字符串。如此一来，就删除了所有行首的\t。

