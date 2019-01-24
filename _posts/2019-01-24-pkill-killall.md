```
平时都是kill pid, 有时候挺麻烦的, 虽然也知道killall, pkill命令的存在, 但是总有不确定的感觉, 比如killall a, 会不会把aa kill掉, /usr/bin/a能不能一起kill掉

下面是总结

killall是忽略启动路径, 只匹配可执行文件名, 所以a和/usr/bin/a会一起kill掉
killall可执行文件名需要全等, killall a不会kill aa, 需要正则的时候就使用-r, 默认信号是SIGTERM

pkill的功能就强大很多, 可以根据各种不同的条件来kill
-g Only match processes in the process group IDs listed
-f 带上参数一起
-n 所有进程的最新
-o 最旧
-P 父进程是多少
-s session id来匹配
-t terminal来匹配
其他看man


```
