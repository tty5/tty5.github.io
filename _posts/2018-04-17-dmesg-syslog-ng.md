# dmesg

dmesg -r 原始信息, -T 显示时间 -L颜色标记重要信息, 一般就是-T, 一直显示就是加上-w

# syslog-ng

dmesg太长的时候, 在syslog-ng的配置目录, 一般是/var/log/kern

syslog-ng定义3个东西, 一个是source, 一个filter, 一个dest

source里面system()包含了一部分dmesg, 比较凌乱, 简单一点就是这样

```
source s_sys {
    #system();
    internal();
    file ("/proc/kmsg" program_override("kernel: "));
    # udp(ip(0.0.0.0) port(514));
};
```

filter
```
filter f_kernel     { facility(kern); };
```

dest
```
log { source(s_sys); filter(f_kernel); destination(d_kern); };
```
