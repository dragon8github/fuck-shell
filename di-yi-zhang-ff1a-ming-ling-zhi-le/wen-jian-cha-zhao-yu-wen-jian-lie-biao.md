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

-name 总是用给定的文件名进行匹配。  
-path 则将文件路径作为一个整体进行匹配。例如：

```
$ find /home -path "*/myshell"

/home/myshell
```

选项 -regex 的参数和 -path 的类似，只不过 -regex 是基于正则表达式来匹配文件路径的。

\(5\)使用正则表达式来匹配：

```py
$ ls
new.PY next.jpg test.py
$ find . -regex ".*\(\.py\|\.sh\)$"
./test.py
```

类似地， -iregex 可以让正则表达式忽略大小写。例如：

```
$ find . -iregex ".*\(\.py\|\.sh\)$"
./test.py
./new.PY
```

\(6\) 否定参数

下面的 find 命令能够匹配所有不以.txt结尾的文件名

```
$ find . ! -name "*.txt"
```

\(7\) 控制查找目录深度

大多数情况下，我们只需要在当前目录中进行搜索，无须再继续向下查找。对于这种情况， 我们使用深度选项来限制 find 命令向下查找的深度。如果只允许 find 在当前目录中查找，深度 可以设置为 1 ；当需要向下两级时，深度可以设置为2；其他情况可以依次类推。

```
$ find . -maxdepth 1
```

\(8\) 根据文件类型搜索

Unix类系统将一切都视为文件。文件具有不同的类型，例如普通文件、目录、字符设备、块 设备、符号链接、硬链接、套接字以及FIFO等。

只列出所有的目录：

```
$ find . -type d -print
```

只列出普通文件：

```
$ find . -type f -print
```

![](/assets/impor12123123123t.png)

\(9\) 根据文件时间进行搜索

Unix/Linux文件系统中的每一个文件都有三种时间戳，如下所示。

* 访问时间（ -atime ） ：用户最近一次访问文件的时间。
* 修改时间（ -mtime ） ：文件内容最后一次被修改的时间。
* 变化时间（ -ctime ） ：文件元数据（例如权限或所有权）最后一次改变的时间。



