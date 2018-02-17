在日常工作中使用shell时，有时候命令只有满足某些条件或是某种外部事件（例如文件可以被下载）操作才能够成功执行。这种情况下，你可能希望重复执行命令，直到成功为止。

```py
repeat()
{
	while true
	do
		$@ && return
	done
}

repeat() { while true; do $@ && return; done }
```



