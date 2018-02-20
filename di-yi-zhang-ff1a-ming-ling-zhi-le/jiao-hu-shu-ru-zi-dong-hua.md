### 交互输入自动化

就编写自动化工具或测试工具而言，实现命令的交互输入自动化极其重要。在很多情况下， 我们要同一些以交互方式读取输入的命令打交道。下面的例子就是一个要求提供交互式输入的命 令执行过程。

```bash
$ command
Enter a first-name: lee
Enter last-name: mp
hello world!! lee mp
```

先写一个读取交互式输入的脚本，然后用这个脚本进行自动化的演示：

```py
#!/bin/bash
#文件名: interactive.sh
read -p "Enter first-name:" a ;
read -p "Enter last-name:" b
echo Hello world $a $b;
```

执行结果：

```
$ ./interactive.sh
Enter first-name:lee
Enter last-name:mp
Hello world lee mp
```

### 用echo -e来生成输入序列

```
$ echo -e "1\nhello\n" > input.data
$ cat input.data
1
hello
```

然后我们就可以从文件中导入交互式输入数据：

```
$ ./interactive.sh < input.data
```



