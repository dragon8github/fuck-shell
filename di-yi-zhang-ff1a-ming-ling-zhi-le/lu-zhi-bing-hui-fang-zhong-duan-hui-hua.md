当你需要为别人在终端上演示某些操作或是需要准备一个命令行教程时， 通常得一边手动输 入命令一边演示，或者也可以录制一段屏幕演示视频，然后再回放出来。其实也有其他的实现方 法。利用 script 和 scriptreplay 命令，我们可以录制命令的次序以及时序，将相关数据记录 在文本文件中。利用这些文件，其他人可以在终端上回放并查看命令的输出。

```py
$ script -t 2> timing.log -a output.session 
Script started, file is output.session # 开始你的表演

# 这里是你表演的舞台

$ exit
Script done, file is output.session # 停止你的表演
```

两个配置文件被当做 script 命令的参数。其中一个文件（timing.log）用于存储时序信息，描述每一个命令在何时运行；另一个文件（output.session）用于存储命令输出。 -t 选项用于将时序数据导入 stderr 。 2&gt; 则用于将 stderr 重定向到timing.log。

利用这两个文件：timing.log（存储时序信息）和output.session（存储命令输出信息） ，我们可以按照下面的方法回放命令执行过程：

```py
$ scriptreplay timing.log output.session # 按播放命令序列输出
```



