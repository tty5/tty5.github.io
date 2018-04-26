# 记录task执行, 被换出去过程
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
