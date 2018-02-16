在编写脚本的时候会频繁使用标准输入（ stdin ） 、标准输出（ stdout ）和标准错误（ stderr ） 。

通过内容过滤将输出重定向到文件是我们平日里的基本任务之一。

*  0 —— stdin （标准输入）
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

3、来看看什么是标准错误以及如何对它重定向

```
$ ls +
ls: cannot access +: No such file or directory

$ ls + 2> out.txt # 正常运行
$ cat ./out.txt
ls: cannot access +: No such file or directory


```



