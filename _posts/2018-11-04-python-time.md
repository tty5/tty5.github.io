# python 时间处理
python的时间有三种类型
- timestamp 浮点数 没有时区概念
- 时间元组 年月日结构体 有时区概念
- 时间字符串

## timestamp

```
获得timestamp

time.time()
1541415735.62

timestamp -> datetime

datetime.datetime.fromtimestamp(1541415735.62)
datetime.datetime(2018, 11, 5, 19, 2, 15, 620000)

datetime -> str
datetime.datetime.fromtimestamp(1541415735.62).strftime("%Y-%m-%d %H:%M:%S.%f")
```
