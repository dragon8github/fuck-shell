### 逗号分隔型数值（Comma Separated Value，CSV）数据条目循环

```
oldIFS=$IFS
IFS=,

for item in $data;
do
echo Item: $item
done

IFS=$oldIFS
```

输出结果：

Item: name

Item: sex

Item: rollno

Item: location

IFS的默认值为空白字符（换行符、制表符或者空格） 。

当IFS被设置为逗号时，shell将逗号视为一个定界符，因此变量 $item 在每次迭代中读取由

逗号分隔的子串作为变量值。

如果没有把IFS设置成逗号，那么上面的脚本会将全部数据作为单个字符串打印出来

