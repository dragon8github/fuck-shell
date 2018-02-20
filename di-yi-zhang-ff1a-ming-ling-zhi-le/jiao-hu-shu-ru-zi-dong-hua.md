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

#### 用echo -e来生成输入序列

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

是不是很棒棒~~！

### 用expect实现交互自动化测试

在默认情况下，多数常见的Linux发行版中并不包含expect。你得用软件包管理器手动进行 安装。

> yum install -y expect

expect等待特定的输入提示，通过检查输入提示来发送数据。

```py
#!/usr/bin/expect
#文件名: automate_expect.sh
spawn ./interactive.sh
expect "Enter first-name:"
send "lee\n"
expect "Enter last-name:"
send "mp\n"
expect eof
```

* spawn参数指定需要自动化哪一个命令；
* expect参数提供需要等待的消息；
* send是要发送的消息；
* expect eof指明命令交互结束。

 运行结果如下： $ ./automate\_expect.sh

```
spawn ./interactive.sh
Enter first-name:lee
Enter last-name:mp
Hello world lee mp
```



