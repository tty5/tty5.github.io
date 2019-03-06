# perf

http://www.brendangregg.com/perf.html

perf record -F 997 -e cpu-clock  -ag  sleep 10000

perf record -F 99  --call-graph dwarf ./a.out 可以打印内核栈到用户态的栈

perf list 列出所有的事件

```
-p 指定进程, 不指定就是后面的进程
-a 表示整个系统, 不单独指定进程
-g 需要调用栈
```

perf script 把所有的事件打印出来

perf report进入交互界面, -s parent可以看到每个函数的百分比, 以及分别分布在哪些栈上


## 用户态

添加probe perf probe -x ./a.out --add 'zzz=main+0x10 a'

perf record -e probe_a:zzz --call-graph dwarf ./a.out

## 一直输出

```
perf record --no-buffering -e probe:do_execve -a -o - | PAGER="cat -v" stdbuf -oL perf script -i -
```

# sched 记录task执行, 被换出去过程
python
```
#!/usr/bin/python

import time

time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
time.sleep(1)
```

## cmd
```
perf record -e sched:sched_switch  -a -- python 1.py
```

## grep对应的task name 和pid
```
          python 24400 [003] 23761.673341: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23762.674350: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23762.674362: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23763.675370: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23763.675385: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23764.676393: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23764.676404: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23765.677414: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23765.677426: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23766.678431: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23766.678441: sched:sched_switch: python:24400 [120] S ==> swapper/3:0 [120]
         swapper     0 [003] 23767.679446: sched:sched_switch: swapper/3:0 [120] R ==> python:24400 [120]
          python 24400 [003] 23767.681327: sched:sched_switch: python:24400 [120] x ==> swapper/3:0 [120]
```

## 如果需要知道每次睡眠的原因的话, 调用栈就是原因, 可以把唤醒的调用栈也加上
```
perf record -e sched:sched_switch  -a --call-graph dwarf -- python 1.py
```
