1、调试shell脚本

2、alias别名

3、53页（增加延时）

4、74页xargs补充内容

5、66页加解密内容，centos7中没有。先删除备份吧

#### 1.crypt是一个简单的加密工具，它从stdin接受一个文件以及口令作为输入，然后将加密 数据输出到Stdout（因此要对输入、输出文件使用重定向）。

```py
$ crypt <input_file >output_file
Enter passphrase: 

# 它会要求输入一个口令。我们也可以通过命令行参数来提供口令。
$ crypt PASSPHRASE <input_file >encrypted_file 

# 如果需要解密文件，可以使用：
$ crypt PASSPHRASE -d <encrypted_file >output_file
```

#### 2.gpg（GNU隐私保护）是一种应用广泛的工具，它使用加密技术来保护文件，以确保数据 在送达目的地之前无法被读取。这里我们讨论如何加密、解密文件。

> gpg签名同样广泛用于在电子邮件通信中的邮件“签名”，以 证明发送方的真实性。

```py
# 用gpg加密文件：
$ gpg -c filename 

# 该命令采用交互方式读取口令，并生成filename.gpg。使用以下命令解密gpg文件：
$ gpg filename.gpg
```

Base64是一组相似的编码方案，它将ASCII字符转换成以64为基数的形式（radix-64 representation），以可读的ASCII字符串来描述二进制数据。base64命令可以用来编码/解 码Base64字符串。要将文件编码为Base64格式，可以使用：

```py
$ base64 filename > outputfile
# 或者
$ cat file | base64 > outputfile
```

解码Base64数据：

```py
$ base64 -d file > outputfile
# 或者
$ cat base64_file | base64 -d > outputfile
```

#### 3.md5sum与sha1sum都是单向散列算法，均无法逆推出原始数据。它们通常用于验证数据 完整性或为特定数据生成唯一的密钥：

```
$ md5sum file
8503063d5488c3080d4800ff50850dc9 file

$ sha1sum file
1ba02b66e2e557fede8f61b7df282cd0a27b816b file
```

> ### 这种类型的散列算法是存储密码的理想方案。
>
> 密码使用其对应的散列值来存储。如果某 个用户需要进行认证，读取该用户提供的密码并转换成散列值，然后将其与之前存储的 散列值进行比对。如果相同，用户就通过认证，被允许访问；否则，就会被拒绝访问。 将密码以明文形式存储是件非常冒险的事，会面临安全风险。

#### 4.shadow-like散列（salt散列）

在Linux中，用户密码是以散列值形式存 储在文件 /etc/shadow中的。该文件中的典型内容类似于下面这样：

```
test:$6$fG4eWdUi$ohTKOlEUzNk77.4S8MrYe07NTRV4M3LrJnZP9p.qc1bR5c.EcOruzPXfEu1uloB FUa18ENRH7F70zhodas3cR.:14790:0:99999:7:::
```

其中 `test:`后面所有的密文就是密码对应的shadow散列值。

