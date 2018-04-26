# install

yum install kexec-tools crash yum-utils -y

systemctl status kdump

systemctl start kdump

vmcore路径在/etc/kdump.conf文件里面

# crash

## config
直接全部打印 set scroll off

## ps
```
> 表示这个cpu当前running的task
ps -p pid或者comm名 显示父进程继承关系
ps -c 显示子进程
ps comm 显示这种进程的task
ps -t task运行时间
ps -k kernel task
ps -S 进程个数总结
ps -l 显示task最后到达时间
ps -a显示命令行和环境变量
ps -r resource limit
```
## log
```
显示dmesg
```
## set
```
set 显示当前 pid
set pid 切换pid
set -v 显示crash变量
```

## bt
```
bt -a显示每个cpu上活动task的调用栈
bt -c 限定cpu显示task调用栈
bt task_address pid 显示他们的调用栈
bt -f 显示栈
bt -F显示栈, 把栈里面的内容解析成符号, 不一定好用
```

## dis
```
dis 显示汇编
dis -l 源代码行号显示
dis -r 给一个地址, 向前显示函数, -f, 向后显示函数
dis -u 用户态地址
dis -x 16进制显示数字
dis -s address 显示这个地址的源代码对应的地方
总结起来, 给了一个地址, 想看源代码内容就是-s, 只对应行号, 那就是向前, 向后-lr, -lf查看
```

# vm
```
vm 显示一个task的vm映射情况
vm -m 显示mm_struct结构体内容
vm -v 遍历vm_area_struct显示里面的内容
vm -f 解析vm flags
vm -p 每个页的映射情况都打印出来
vm -P vma 只打印一个vma的映射情况
```

# foreach
```
foreach pid taskp name user kernel RU IN UN 等来执行命令, 命令有bt ps等
foreach默认是所有的task
```

# files
```
显示task打开的文件描述符
```
