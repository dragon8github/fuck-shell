CSV数据条目循环

```
data="name,sex,rollno,location"
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

