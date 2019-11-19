# 断点到固定进程
```
b do_fault if $_streq($lx_current()->comm, "a.out")

gdb vmlinux -ex 'target remote :5'

CFLAGS_filemap.o=-Og

__attribute__((optimize("-O0")))
```
https://sourceware.org/gdb/current/onlinedocs/gdb/Convenience-Funs.html#Convenience-Funs

# gcc O0
```
#!/bin/sh
for file in $@
do
    LINENUM=1
    sed -i "$LINENUM i#pragma GCC optimize(\"O0\")" $file
done


exit 0

#__attribute__((optimize("-O0")))

for file in $@
do
    LINENUM=`sed -n '/^#include / =' $file|sed -n '$ p'`
    if [ -z "$LINENUM" ]
    then
        LINENUM=1
    fi

    sed -i "$LINENUM a#pragma GCC optimize(\"O0\")" $file
done
```

# 如何找到proc文件sys文件对应的内核函数

* 工作中, 经常会读取proc或者sys目录下的很多文件, 比如cat /proc/cmdline, cat /proc/uptime之类的,
* 有时候我们想看看对应的内核实现, 却不知道从哪里找起, 老司机们当然很容易从源代码中根据经验和某种规律找出来
* 但是新手就困难得多. 下面有一种办法是很容易得获得这些接口文件对应的内核函数

```
trace-cmd

trace-cmd record -p function_graph -g vfs_read cat /proc/cmdline ; trace-cmd report |vim -
```

会记录内核从vfs_read这一层往下调用的所有函数过程, 就很容易找到了

