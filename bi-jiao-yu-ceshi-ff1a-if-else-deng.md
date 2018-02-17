### if 条件

```
if condition;
then
    commands;
fi
```

### else if 和 else

```js
if condition;
then
    commands;
else if condition; then
    commands;
else
    commands;
fi
```

### 算术比较

* -gt ：大于。
* -lt ：小于。
* -ge ：大于或等于。
* -le ：小于或等于。

```py
[ $var -eq 0 ] #当 $var 等于 0 时，返回真
[ $var -ne 0 ] #当 $var 为非 0 时，返回真

[$var -eq 0 ] or [ $var -eq 0]

[ $var1 -ne 0 -a $var2 -gt 2 ] #使用逻辑与-a
[ $var1 -ne 0 -o var2 -gt 2 ] #逻辑或 -o
```

### 文件系统相关测试

* \[ -f $file\_var \] ：如果给定的变量包含正常的文件路径或文件名，则返回真
* \[ -x $var \] ：如果给定的变量包含的文件可执行，则返回真。
* \[ -d $var \] ：如果给定的变量包含的是目录，则返回真。
* \[ -e $var \] ：如果给定的变量包含的文件存在，则返回真。
* \[ -c $var \] ：如果给定的变量包含的是一个字符设备文件的路径，则返回真
* \[ -b $var \] ：如果给定的变量包含的是一个块设备文件的路径，则返回真。
* \[ -w $var \] ：如果给定的变量包含的文件可写，则返回真。
* \[ -r $var \] ：如果给定的变量包含的文件可读，则返回真。
* \[ -L $var \] ：如果给定的变量包含的是一个符号链接，则返回真。

```
fpath="/etc/passwd"
if [ -e $fpath ]; then
    echo File exists;
else
    echo Does not exist;
fi
```

### 字符串比较

**使用字符串比较时，最好用双中括号**，因为有时候采用单个中括号会产生错误，所以最好避开它们。

* \[\[ $str1 = $str2 \]\] ：当 str1 等于 str2 时，返回真。也就是说， str1 和 str2 包含  的文本是一模一样的。
* \[\[ $str1 == $str2 \]\] ：这是检查字符串是否相等的另一种写法。  也可以检查两个字符串是否不同。
* \[\[ $str1 != $str2 \]\] ：如果 str1 和 str2 不相同，则返回真。  我们还可以检查字符串的字母序情况，具体如下所示。
* \[\[ $str1 &gt; $str2 \]\] ：如果 str1 的字母序比 str2 大，则返回真。
* \[\[ $str1 &lt; $str2 \]\] ：如果 str1 的字母序比 str2 小，则返回真。
* \[\[ -z $str1 \]\] ：如果 str1 包含的是空字符串，则返回真。
* \[\[ -n $str1 \]\] ：如果 str1 包含的是非空字符串，则返回真。





