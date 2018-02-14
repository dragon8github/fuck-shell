### echo

无论单引号，双引号，无引号都是可以打印的。只要没有特殊符号。

```
$ echo "Welcome to Bash"
$ echo 'Welcome to Bash'
$ echo Welcome to Bash
```

### printf

```
#!/bin/bash
#文件名: printf.sh
printf "%-5s %-10s %-4s\n" No Name Mark
printf "%-5s %-10s %-4.2f\n" 1 Sarath 80.3456
printf "%-5s %-10s %-4.2f\n" 2 James 90.9989
printf "%-5s %-10s %-4.2f\n" 3 Jeff 77.564
```

我们会得到如下格式化的输出：

![](/assets/import.png)

%-5s 指明了一个格式为左对齐且宽度为5的字符串替换（ - 表示左对齐） 。如果不用 - 指定对齐方式，字符串就采用右对齐形式。

对于浮点数%f，可以使用其他参数对小数部分进行舍入。

对于 Mark 字段，将其格式化为 %-4 . 2f ，其中. 2 指定保留2个小数位

