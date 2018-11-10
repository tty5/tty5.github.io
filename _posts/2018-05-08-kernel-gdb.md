# 断点到固定进程
```
b do_fault if $_streq($lx_current()->comm, "a.out")

gdb vmlinux -ex 'target remote :5'

CFLAGS_filemap.o=-Og

__attribute__((optimize("-O0")))
```
https://sourceware.org/gdb/current/onlinedocs/gdb/Convenience-Funs.html#Convenience-Funs
