#### 加密工具与散列

加密技术主要用于防止数据遭受未经授权的访问。 加密算法有很多，我们会着重讲解那些常 见的标准加密算法：

* crypt
* gpg
* base64
* md5sum
* sha1sum
* openssl

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

```
# 用gpg加密文件：
$ gpg -c filename 

# 该命令采用交互方式读取口令，并生成filename.gpg。使用以下命令解密gpg文件：
$ gpg filename.gpg 
```



