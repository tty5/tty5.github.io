# 断点到固定进程
```
b do_fault if $_streq($lx_current()->comm, "a.out")
```

https://sourceware.org/gdb/current/onlinedocs/gdb/Convenience-Funs.html#Convenience-Funs
