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
