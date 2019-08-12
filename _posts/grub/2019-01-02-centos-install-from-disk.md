# centos 硬盘安装

- 把iso拷贝到一个分区的/下, 比如vdb, vdax也可以, 只是vdax这个分区在安装的时候不能用了
- 把iso文件里面的isolinux/vmlinuz, initrd.img拷贝出来, 放在/boot下, 比如vmlinuz-xxx, initrd.img-xxx, 更新grub.cfg
- 这个vmlinuz和initrd.img对应的启动项加参数inst.stage2=hd:/dev/vdb, inst.repo也是可以的, 更全, 删除cmd的root=

# 网卡名字

- kernel cmdlinux add net.ifnames=0 biosdevname=0
