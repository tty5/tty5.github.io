# bash || && 后面接多命令

```
suc echo 123 && {echo 123; echo 456}

fail echo 123 || {echo 123; echo 456}
```

# 箭头
```
> 写入文件
>> append文件

< 读取文件
<< 输入结束符

cat <<eof |md5sum
123
333eof
```
