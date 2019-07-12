# centos 硬盘安装

- 把iso拷贝到一个分区的/下, 比如vda1
- 把iso文件里面的isolinux/vmlinuz, initrd.img拷贝出来, 放在/boot下, 比如vmlinuz-xxx, initrd.img-xxx, 更新grub.cfg
- 这个vmlinuz和initrd.img对应的启动项加参数inst.stage2=hd:/dev/vda1

