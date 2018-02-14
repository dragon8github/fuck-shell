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

No    Name       Mark

1     Sarath     80.35

2     James      91.00

3     Jeff       77.56







