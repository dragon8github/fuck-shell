\(1\) 读取日期：

```
$ date
Sat Feb 17 08:50:10 CST 2018
```

\(2\)获取当前时间戳：

```
$ date +%s
1518828637
```

\(3\)获取指定时间的时间戳：

```
$ date --date "2018/2/17 8:51:32" +%s
1518828692
```

\(4\)获取指定时间是星期几：

```
$ date --date "2018/2/17" +%A
Saturday
```

\(5\)自定义时间格式：

```
$ date "+%Y-%m-%d %H:%M:%S"
2018-02-17 08:56:08
```

### 实战演练

有时候，我们需要检查一组命令所花费的时间，可以使用以下代码：

```py
#!/bin/bash
#文件名: time_take.sh
start=$(date +%s)

echo "这里写上你要测试的语句"

end=$(date +%s)
difference=$(( end - start))
echo Time taken to execute commands is $difference seconds.
```

![](/assets/import223123123.png)

