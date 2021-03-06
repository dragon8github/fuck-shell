### 数组和关联数组

数组是shell脚本非常重要的组成部分，它借助索引将多个独立的数据存储为一个集合。

普通数组只能使用整数作为数组索引。Bash也支持关联数组，它可以使用字符串作为数组索引。

#### 普通数组

\(1\) 定义数组的方法有很多种。可以在单行中使用一列值来定义一个数组：

```
$ arr=(1 2 3 4 5 6)
```

也可以这样定义：

```
$ arr[0]='hello'
$ arr[1]='world'
```

\(2\) 打印出特定索引的数组元素内容：

```
echo ${arr[1]}
```

\(3\) 以清单形式打印出数组中的所有值：

```
$ echo ${arr[@]} 
1 2 3 4 5 6

$ echo ${arr[*]}
1 2 3 4 5 6
```

\(4\) 打印数组长度：

```
$ echo ${#arr[*]}
6
```

#### 关联数组

1. 定义关联数组：

```
$ declare -A ass_array
```

2.添加元素

```
$ ass_array['hello']='world'
```

3.读取元素

```
$ echo ${ass_array['hello']}
world
```

还可以 利用内嵌“索引 - 值”列表的方法，提供一个“索引 - 值”列表：

```
$ declare -A fruits_value
$ fruits_value=(['apple']=100, ['watermelon']=200)

$ echo ${fruits_value[@]}
100, 200
```

4、列出索引数组的所有索引：

```
$ echo ${!fruits_value[@]}
apple watermelon

$ echo ${!fruits_value[*]}
apple watermelon
```



