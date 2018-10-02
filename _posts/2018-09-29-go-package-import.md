# go package搜索路径

写了绝对路径的, 就是绝对路径

如果是import本地package
```
import ./xx
```

没写的, 顺序

```
vendor
goroot
gopath
```
