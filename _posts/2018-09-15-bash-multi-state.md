# bash || && 后面接多命令

```
suc [[ 1 ]] && { echo "yes-1"; echo "yes-2"; }

fail [[ 1 ]] || { echo "yes-1"; echo "yes-2"; }
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
