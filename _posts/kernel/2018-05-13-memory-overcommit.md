# memory overcommit

proc文件是/proc/sys/vm/overcommit_memory
- 0 Heuristic overcommit handling
- 1 Always overcommit
- 2 Don’t overcommit

0的时候是由函数__vm_enough_memory来判断是否给申请内存

遇到这种问题, 直接改成1就完了
