### 分割文件和数据

在某些情况下，必须把文件分割成多个更小的片段。早期像软盘之类的设备容量都很有限， 将文件分割得更小些，以便能够存储到多张磁盘中就显得至关重要了。不过如今我们分割文件就 是出于其他目的了，比如为提高可读性、生成日志、通过E-mail发送文件等。在这则攻略中我们 会看到将文件分割成不同大小的多种方法。

##### 1.假设有一个叫做data.file的测试文件，其大小为100KB。你可以将该文件分割成多个大小为10KB的文件，方法如下：

```
$ split -b 10k data.file 
$ ls
data.file xaa xab xac xad xae xaf xag xah xai xaj
```

上面的命令将data.file分割成多个文件，每一个文件大小为10KB。这些文件以xab、xac、xad的 形式命名。这表明它们都有一个字母后缀。 如果想以数字为后缀，可以另外使用-d参数。此外， 使用 -a length可以指定后缀长度：

```
$ split -b 10k data.file -d -a 4 
$ ls
data.file x0009 x0019 x0029 x0039 x0049 x0059 x0069 x0079
```

除了k（KB）后缀，我们还可以使用M（MB）、G（GB）、c（byte）、w（word）等后缀。

##### 2. 为分割后的文件指定文件名前缀

```
$ split [COMMAND_ARGS] PREFIX
```

我们加上文件名前缀再运行先前那个命令来分割文件：

```
$ split -b 10k data.file -d -a 4 split_file
$ ls
data.file split_file0002 split_file0005 split_file0008 strtok.c
split_file0000 split_file0003 split_file0006 split_file0009
split_file0001 split_file0004 split_file0007
```

##### 3. 如果不想按照数据块大小，而是需要根据行数来分割文件的话，可以使用 -l no\_of\_lines：

```
$ split -l 10 data.file # 分割成多个文件，每个文件包含10行
```

### csplit

另一个有趣的的工具是csplit。它能够依据指定的条件和字符串匹配选项对日志文件进行 分割。

csplit是split工具的一个变体。split只能够根据数据大小或行数分割文件，而csplit 可以根据文本自身的特点进行分割。是否存在某个单词或文本内容都可作为分割文件的条件。

看一个日志文件示例：

```py
$ cat server.log
SERVER-1
[connection] 192.168.0.1 success
[connection] 192.168.0.2 failed
[disconnect] 192.168.0.3 pending
[connection] 192.168.0.4 success
SERVER-2
[connection] 192.168.0.1 failed
[connection] 192.168.0.2 failed
[disconnect] 192.168.0.3 success
[connection] 192.168.0.4 failed
SERVER-3
[connection] 192.168.0.1 pending
[connection] 192.168.0.2 pending
[disconnect] 192.168.0.3 pending
[connection] 192.168.0.4 failed
```

我们需要将这个日志文件分割成server1.log、server2.log和server3.log，这些文件的内容分别 取自原文件中不同的SERVER部分。那么，可以使用下面的方法来实现：

```
$ csplit server.log /SERVER/ -n 2 -s {*} -f server -b "%02d.log" ; rm server00.log
$ ls
server01.log server02.log server03.log server.log
```

有关这个命令的详细说明如下：

* /SERVER/ 用来匹配某一行，分割过程即从此处开始。
* /\[REGEX\]/ 表示文本样式。包括从当前行（第一行）直到（但不包括）包含“SERVER” 的匹配行。
* {\*} 表示根据匹配重复执行分割，直到文件末尾为止。可以用{整数}的形式来指定分割执 行的次数。
* -s 使命令进入静默模式，不打印其他信息。
* -n 指定分割后的文件名后缀的数字个数，例如01、02、03等。
* -f 指定分割后的文件名前缀（在上面的例子中，server就是前缀）。
* -b 指定后缀格式。例如%02d.log，类似于C语言中printf的参数格式。在这里文件名= 前缀+后缀=server + %02d.log。

 因为分割后的第一个文件没有任何内容（匹配的单词就位于文件的第一行中），所以我们删 除了server00.log。

