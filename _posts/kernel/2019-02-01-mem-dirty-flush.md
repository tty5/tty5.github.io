# dirty控制参数

dirty_background_bytes 后台开始刷的触发点
dirty_background_ratio

dirty_bytes 前台
dirty_ratio

dirty_expire_centisecs 脏页超时时间
dirty_writeback_centisecs 周期回刷时间


# memory overcommit

proc文件是/proc/sys/vm/overcommit_memory
- 0 Heuristic overcommit handling
- 1 Always overcommit
- 2 Don’t overcommit

0的时候是由函数__vm_enough_memory来判断是否给申请内存

遇到这种问题, 直接改成1就完了


# oom
```
[  122.078526] python invoked oom-killer: gfp_mask=0xd0, order=0, oom_score_adj=0
[  122.079475] python cpuset=/ mems_allowed=0
[  122.079960] CPU: 6 PID: 1399 Comm: python Not tainted 3.10.0-693.21.1.el7.x86_64 #1
[  122.080832] Hardware name: QEMU Standard PC (i440FX + PIIX, 1996), BIOS 0.5.1 01/01/2011
[  122.081842] Call Trace:
[  122.082140]  [<ffffffff816ae7c8>] dump_stack+0x19/0x1b
[  122.082744]  [<ffffffff816a9b90>] dump_header+0x90/0x229
[  122.083358]  [<ffffffff811f5fc4>] ? try_get_mem_cgroup_from_mm+0x34/0x60
[  122.084240]  [<ffffffff811f5fb8>] ? try_get_mem_cgroup_from_mm+0x28/0x60
[  122.085092]  [<ffffffff8118a884>] oom_kill_process+0x254/0x3d0
[  122.085838]  [<ffffffff811f9cd6>] mem_cgroup_oom_synchronize+0x546/0x570
[  122.086717]  [<ffffffff811f9150>] ? mem_cgroup_charge_common+0xc0/0xc0
[  122.087478]  [<ffffffff8118b114>] pagefault_out_of_memory+0x14/0x90
[  122.088201]  [<ffffffff816a7f2e>] mm_fault_error+0x68/0x12b
[  122.088916]  [<ffffffff816bb741>] __do_page_fault+0x391/0x450
[  122.089587]  [<ffffffff816bb8e6>] trace_do_page_fault+0x56/0x150
[  122.090274]  [<ffffffff816baf7a>] do_async_page_fault+0x1a/0xd0
[  122.090962]  [<ffffffff816b7798>] async_page_fault+0x28/0x30
[  122.091618] Task in /foo killed as a result of limit of /foo
[  122.092279] memory: usage 1048576kB, limit 1048576kB, failcnt 677
[  122.092991] memory+swap: usage 1048576kB, limit 9007199254740988kB, failcnt 0
[  122.093820] kmem: usage 0kB, limit 9007199254740988kB, failcnt 0
[  122.094510] Memory cgroup stats for /foo: cache:56KB rss:1048520KB rss_huge:1038336KB mapped_file:0KB swap:0KB inactive_anon:0KB active_anon:1048520KB inactive_file:28KB active_file:28KB unevictable:0KB
[  122.096721] [ pid ]   uid  tgid total_vm      rss nr_ptes swapents oom_score_adj name
[  122.097647] [ 1243]     0  1243    29143      850      13        0             0 bash
[  122.098608] [ 1399]     0  1399  1007354   262500     527        0             0 python
[  122.099537] Memory cgroup out of memory: Kill process 1399 (python) score 973 or sacrifice child
[  122.100541] Killed process 1399 (python) total-vm:4029416kB, anon-rss:1048144kB, file-rss:1856kB, shmem-rss:0kB
```

## 查看
先看是哪个memcg满了, 然后看哪个memcg的task被kill掉了, 基本上都是file-cache没了, 全是匿名页

一般一个memcg就是cache和rss, cache就是文件页, rss分为文件页和匿名页, 匿名页太多, 回收失败

dump_tasks打印出所有的task mem情况

最后挑一个kill


# ext4 read
```
vfs_read -> file->f_op->read_iter [ext4_file_read_iter] 里面 要么 dax函数, 要么generic_file_read_iter

generic_file_read_iter里面要么direct io, 要么, do_generic_file_read

do_generic_file_read就是通用的page cache函数, 申请, 找到页, 用mapping->a_ops->readpage[ext4_readpage]填充页, 然后把页add_to_page_cache_lru

总结起来就是ext4_file_read_iter的读函数用了page cache来读数据, 并提供了ext4_readpage让page cache模块来读自己的页
```

# 块设备 read
```
其他都一样, file->f_op->read_iter[blkdev_read_iter], mapping->a_ops->readpage[blkdev_readpage]
```

# 哪些算buffer
```
所有的file cache, 算整体, 减去块设备链表上的块设备的page, 就是cache, 块设备上的page算buffer
```

# vma映射

每个vma映射空间都有一个vma->vm_ops[<ext4_file_vm_ops], stack空间有自己的操作函数, 文件映射空间有自己的操作函数, 在这些函数里面, 要么申请一个page cache来填充这个映射, 要么就是一个匿名页
