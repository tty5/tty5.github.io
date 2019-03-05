---
categories: linux-cmd
---

# console tty 区别
tty teletypewriter, linux里面有输入, 输出的设备, 现在基本都是虚拟设备, pts之类的

console, 特殊的tty, 可以显示系统日志的, 比如刚开机

# 获取当前tty
```
tty
/dev/pts/15
```
# 检查是否是一个tty
```
tty -s
echo $?
```

# dump tty info
```
$stty -a
speed 38400 baud; rows 65; columns 231; line = 0;
```
