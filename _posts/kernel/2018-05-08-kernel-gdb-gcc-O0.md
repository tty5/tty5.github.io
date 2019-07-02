# 断点到固定进程
```
b do_fault if $_streq($lx_current()->comm, "a.out")

gdb vmlinux -ex 'target remote :5'

CFLAGS_filemap.o=-Og

__attribute__((optimize("-O0")))
```
https://sourceware.org/gdb/current/onlinedocs/gdb/Convenience-Funs.html#Convenience-Funs

# gcc O0
```
#!/bin/sh
for file in $@
do
    LINENUM=1
    sed -i "$LINENUM i#pragma GCC optimize(\"O0\")" $file
done


exit 0

#__attribute__((optimize("-O0")))

for file in $@
do
    LINENUM=`sed -n '/^#include / =' $file|sed -n '$ p'`
    if [ -z "$LINENUM" ]
    then
        LINENUM=1
    fi

    sed -i "$LINENUM a#pragma GCC optimize(\"O0\")" $file
done
```
