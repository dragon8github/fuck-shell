find 是Unix/Linux命令行工具箱中最棒的工具之一。该命令对于编写shell脚本所起到的功用  
不可小视，但是多数人却无法最大程度发挥它的功效。这则攻略讨论了 find 的大多数常见用法。

\(1\) 列出当前目录及子目录下所有的文件和文件夹

```
$ find nginx80

nginx80
nginx80/www
nginx80/www/index.html
nginx80/conf
nginx80/conf/nginx.conf
```

\(2\) 根据文件名或正则表达式进行搜索

```
$ find /home -name "*.sh"

/home/myshell/sleep.sh
/home/myshell/variables.sh
/home/myshell/time_take.sh
/home/myshell/printf.sh
/home/myshell/pwd.sh
/home/myshell/isroot.sh
/home/myshell/log.sh
```

**find 命令有一个选项  -iname （忽略字母大小写） ，该选项的作用和  -name 类似，只不过在  
匹配名字时会忽略大小写。**

\(3\) 如果想匹配多个条件中的一个，可以采用OR条件操作：

```
$ find /home -name "*.txt" -o -name "*.sh"

/home/myshell/sleep.sh
/home/myshell/variables.sh
/home/myshell/time_take.sh
/home/myshell/file.txt
/home/myshell/printf.sh
/home/myshell/pwd.sh
/home/myshell/isroot.sh
/home/myshell/log.sh
```

也推荐加入\\( 以及 \\) 用于将 -name "\*.txt" -o -name "\*.sh" 视为一个整体。

```
$ find /home \( -name "*.txt" -o -name "*.sh" \)
```

\(4\)匹配路径

 -name 总是用给定的文件名进行匹配。-path 则将文件路径作为一个整体进行匹配。例如：

```
$ find /home -path "*/myshell"

/home/myshell

```



