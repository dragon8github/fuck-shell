##  临时文件命名与随机数

编写shell脚本时，我们经常需要存储临时数据。最适合存储临时数据的位置是 /tmp（该目录中的内容在系统重启后会被清空）。有两种方法可以为临时数据生成标准的文件名。

####  \(1\) 创建临时文件：

```py
$ filename=`mktemp` 
$ echo $filename 
/tmp/tmp.8xvhkjF5fH
```

####  \(2\) 创建临时目录： 

    $ dirname=`mktemp -d` 
    $ echo $dirname 
    tmp.NI8xzW7VRX

####  \(3\) 如果仅仅是想生成文件名，又不希望创建实际的文件或目录，方法如下：

    $ tmpfile=`mktemp -u`
    $ echo $tmpfile
    /tmp/tmp.RsGmilRpcT 



