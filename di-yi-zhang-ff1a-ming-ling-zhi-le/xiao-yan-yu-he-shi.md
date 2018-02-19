1. 校验和（checksum）用来从文件中生成校验和密钥，然后利用这个校验和密钥核实文件的完整性。
2. 文件可以通过网络或任何存储介质分发到不同的地点。出于多种原因，数据有可能在传输过程中丢失了若干位，从而导致文件损坏。这种错误通常发生在从Internet上下载文件，通过网络传输文件，或者CD光盘损坏等。因此，我们需要采用一些测试方法来确定接收到的文件是否存在错误。用于文件完整性测试的特定密钥就称为校验和。
3. 我们对原始文件和接收到的文件都进行校验和计算。通过比对两者的校验和，就能够核实 接收到的文件是否正确。如果校验和 （一个来自发送地的原始文件， 另一个来自目的地的接收文件） 相等，就意味着我们接收到了正确的文件，否则说明用户接收到的不是正确的文件，可能需要再次获取并校验和。
4. 校验和对于编写备份脚本或系统维护脚本来说非常重要， 因为它们都会涉及通过网络传输文件。 通过使用校验和核实， 我们就可以识别出那些在网络传输过程中出现损坏的文件， 并进行重发。

#### 1.为了计算md5sum，使用下列命令格式：

```py
$ md5sum filename 
68b329da9893e34099c7d8ad5cb9c940 filename

$ md5sum file1 file2 file3 .. 
[checksum1] file1
[checksum1] file2
[checksum1] file3
```

#### 2.将输出的校验和重定向到一个文件，然后用这个MD5文件核实数据的完整性：

```
$ md5sum filename > file_sum.md5
```

#### 3.  用生成的文件核实数据完整性：

```
$ md5sum -c file_sum.md5
```

如果需要用所有的.md5信息来检查所有的文件，可以使用：

```
$ md5sum -c *.md5
```

#### 4. 对目录进行校验

校验和是从文件中计算得来的。对目录计算校验和意味着我们需要对目录中的所有文件以递 归的方式进行计算。 这可以用命令md5deep或sha1deep来实现。首先，需要安装md5deep软件包以确保能找到 这些命令。该命令的用法如下：

* -r使用递归的方式
* -l使用相对路径。默认情况下，md5deep会输出文件的绝对路径

```py
$ md5deep -r -l directory_path > directory.md5
```

或者也可以结合find来递归计算校验和：

```
$ find directory_path -type f -print0 | xargs -0 md5sum >> directory.md5
```

## Example

##### 1.创建一个txt文件并随意填充内容

```py
$ vim filename.txt # 输入一些内容如12345678
```

##### 2.使用md5sum对其加密，然后将生成的md5码放入文件中

```
$ md5sum file.txt > file_sum.md5
```

##### 3.进行检验

```
$ md5sum -c file_sum.md5
file.txt: OK
```

##### 4.试着修改一下filename.txt的内容，然后再试试验证

```
$ vim filename.txt # 修改为内容123

$  md5sum -c file_sum.md5
file.txt: FAILED
md5sum: WARNING: 1 computed checksum did NOT match
```

与md5sum类似，SHA-1是另一种常用的校验和算法。

它从给定的输入文件中生成一个长度 为40个字符的十六进制串。用来计算SAH-1串的命令是sha1sum。

其用法和md5sum的非常相似。 只需要把先前讲过的那些命令中的md5sum替换成sha1sum就行了，记住将输入文件名从 file\_sum.md5改为file\_sum.sha1。

校验和对于核实下载文件的完整性非常有帮助。我们从网上下载的ISO镜像文件一般更容易 出现错误（见图2-1）。为了检查接收文件正确与否，校验和得以广泛应用。校验和程序对同样的 文件数据始终生成一模一样的校验和。

![](/assets/import111.png)

