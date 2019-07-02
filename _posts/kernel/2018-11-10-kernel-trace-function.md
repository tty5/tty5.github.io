# 如何找到proc文件sys文件对应的内核函数

* 工作中, 经常会读取proc或者sys目录下的很多文件, 比如cat /proc/cmdline, cat /proc/uptime之类的,
* 有时候我们想看看对应的内核实现, 却不知道从哪里找起, 老司机们当然很容易从源代码中根据经验和某种规律找出来
* 但是新手就困难得多. 下面有一种办法是很容易得获得这些接口文件对应的内核函数

```
trace-cmd

trace-cmd record -p function_graph -g vfs_read cat /proc/cmdline ; trace-cmd report |vim -
```

会记录内核从vfs_read这一层往下调用的所有函数过程, 就很容易找到了
