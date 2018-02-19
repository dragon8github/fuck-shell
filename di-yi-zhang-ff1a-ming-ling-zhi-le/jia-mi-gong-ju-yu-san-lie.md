####  加密工具与散列

 加密技术主要用于防止数据遭受未经授权的访问。 加密算法有很多，我们会着重讲解那些常 见的标准加密算法：

* crypt
* gpg
* base64
* md5sum
* sha1sum
* openssl

####  1.crypt是一个简单的加密工具，它从stdin接受一个文件以及口令作为输入，然后将加密 数据输出到Stdout（因此要对输入、输出文件使用重定向）。

```py
$ crypt <input_file >output_file
Enter passphrase: 

# 它会要求输入一个口令。我们也可以通过命令行参数来提供口令。
$ crypt PASSPHRASE <input_file >encrypted_file 

# 如果需要解密文件，可以使用：
$ crypt PASSPHRASE -d <encrypted_file >output_file 
```



