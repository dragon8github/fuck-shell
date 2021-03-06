find 是Unix/Linux命令行工具箱中最棒的工具之一。该命令对于编写shell脚本所起到的功用  
不可小视，但是多数人却无法最大程度发挥它的功效。这则攻略讨论了 find 的大多数常见用法。

#### \(1\) 列出当前目录及子目录下所有的文件和文件夹

```
$ find nginx80

nginx80
nginx80/www
nginx80/www/index.html
nginx80/conf
nginx80/conf/nginx.conf
```

#### \(2\) 根据文件名或正则表达式进行搜索

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

find 命令有一个选项  -iname （忽略字母大小写） ，该选项的作用是在匹配名字时会忽略大小写。

#### \(3\) 如果想匹配多个条件中的一个，可以采用OR条件操作：

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

#### \(4\) 匹配路径

-name 总是用给定的文件名进行匹配。  
-path 则将文件路径作为一个整体进行匹配。例如：

```
$ find /home -path "*/myshell"

/home/myshell
```

选项 -regex 的参数和 -path 的类似，只不过 -regex 是基于正则表达式来匹配文件路径的。

#### \(5\)使用正则表达式来匹配：

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

#### \(6\) 否定参数

下面的 find 命令能够匹配所有不以.txt结尾的文件名

```
$ find . ! -name "*.txt"
```

#### \(7\) 控制查找目录深度

大多数情况下，我们只需要在当前目录中进行搜索，无须再继续向下查找。对于这种情况， 我们使用深度选项来限制 find 命令向下查找的深度。如果只允许 find 在当前目录中查找，深度 可以设置为 1 ；当需要向下两级时，深度可以设置为2；其他情况可以依次类推。

```
$ find . -maxdepth 1
```

#### \(8\) 根据文件类型搜索

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

#### \(9\) 根据文件时间进行搜索

Unix/Linux文件系统中的每一个文件都有三种时间戳，如下所示。

* 访问时间（ -atime ） ：用户最近一次访问文件的时间。
* 修改时间（ -mtime ） ：文件内容最后一次被修改的时间。
* 变化时间（ -ctime ） ：文件元数据（例如权限或所有权）最后一次改变的时间。

打印出在最近7天内被访问过的所有文件：

```
$ find . -type f -atime -7
```

打印出在7天前那天被访问过的所有文件：

```
$ find . -type f -atime 7
```

打印出访问时间超过7天的所有文件：

```
$ find . -type f -atime +7
```

类似地，我们可以根据修改时间，用 -mtime 进行搜索，也可以根据变化时间，用 -ctime 进行搜索。

还有其他一些基  
于时间的参数是以分钟作为计量单位的。这些参数包括：

* -amin （访问时间） 
* -mmin （修改时间）
* -cmin （变化时间） 

打印出访问时间超过7分钟的所有文件：

```
$ find . -type f -amin +7
```

#### 比较文件之间的修改时间（时间戳）

find 命令的时间戳处理选项对编写系统备份和维护脚本很有帮助。

找出比file.txt修改时间更近的所有文件：

```
$ find . -type f -newer file.txt
```

#### \(10\) 基于文件大小的搜索

```
$ find . -type f -size +2k
#  大于2KB 的文件

$ find . -type f -size -2k
#  小于2KB 的文件

$ find . -type f -size 2k
#  大小等于2KB 的文件
```

除了 k 之外，还可以用其他文件大小单元。

* b —— 块（512字节） 。
* c —— 字节。
* w —— 字（2字节） 。
* k —— 1024字节。
* M —— 1024K字节。
* G —— 1024M字节。

#### \(11\) 删除匹配的文件

-delete 可以用来删除 find 查找到的匹配文件。

```
$ find . -type f -name "*.swp" -delete
```

#### \(12\) 基于文件权限和所有权的匹配

```
$ find . -type f -perm 644
#  打印出权限为644 的文件
```

以Apache Web服务器为例。Web服务器上的PHP文件需要具有合适的执行权限。我们可以用

下面的方法找出那些没有设置好执行权限的PHP文件：

```
$ find . -type f -name "*.php" ! -perm 644
```

#### \(13\) 根据文件的所有权进行搜索

用选项  -user USER 就能够找出由某个特定用户所拥有  
的文件。参数 USER 可以是用户名或UID。例如，打印出用户root拥有的所有文件：

```
find /home -type f -user root

/home/myshell/sleep.sh
/home/myshell/variables.sh
/home/myshell/time_take.sh
/home/myshell/file.txt
/home/myshell/printf.sh
/home/myshell/pwd.sh
/home/myshell/isroot.sh
/home/myshell/log.sh
```

#### \(14\) find + exec 对搜索结果进行操作

-exec 算得上是 find 最强大的特性之一。

下面的例子中，我们将/home/myshell 下所有的.sh赋予可执行权限

```py
$ find /home/myshell -iname "*.sh" -exec chmod a+x {} \;
```

{} 是一个与  -exec 选项搭配使用的特殊字符串。对于每一个匹配的文件，{} 会被替换成相应的文件名。

另一个例子是将给定目录中的所有sh脚本拼接起来写入单个文件all\_sh\_files.txt。

```
$ find /home/myshell/ -iname "*.sh" -exec cat {} \;>all_sh_file.txt
```

用下列命令将1天前的 .sh文件复制到OLD目录中：

$ mkdir OLD

$ find /home/myshell/ -mtime +1 -name "\*.sh" -exec cp {} OLD \;

#### \(15\)排除指定的目录：

\\( -name ".git" -prune \\) 的作用是用于进行排除，它指明了 .git目录应该被排除在外

```
$ find /home/myshell/ \( -name ".git" -prune \) -o \( -name "*.sh" \)
```



