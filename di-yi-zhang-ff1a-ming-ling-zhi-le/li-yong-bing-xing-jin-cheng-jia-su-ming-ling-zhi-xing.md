###  利用并行进程加速命令执行

 以之前讲过的md5sum命令为例。由于涉及运算，该命令属于CPU密集型命令。如果多个文 件需要生成校验和，我们可以使用下面的脚本来运行md5sum的多个实例。

```bash
#/bin/bash
#文件名: generate_checksums.sh
PIDARRAY=()
for file in File1.iso File2.iso
do
  md5sum $file & 
  PIDARRAY+=("$!")
done
wait ${PIDARRAY[@]}
```

 运行脚本后，可以得到如下输出： 

```
$ ./generate_checksums.sh 
330dcb53f253acdf76431cecca0fefe7 File1.iso
bd1694a6fe6df12c3b8141dcffaf06e6 File2.iso
```

 输出结果和下面命令的结果一样： md5sum File1.iso File2.iso

 但是因为多个md5sum命令是同时运行的，如果你使用的是多核处理器，就会更快地获得运行结 果（可以使用time命令来验证）。

 我们利用了Bash的操作符&，它使得shell将命令置于后台并继续执行脚本。这意味着一旦循 环结束，脚本就会退出，而md5sum命令仍在后台运行。为了避免这种情况，我们使用$!来获得 进程的PID，在Bash中，$!保存着最近一个后台进程的PID。我们将这些PID放入数组，然后使用 wait命令等待这些进程结束。

