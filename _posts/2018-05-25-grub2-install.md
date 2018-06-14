# grub2 install

grub2-install /dev/vda

mbr分区的话 需要在mbr和第一个分区之间留一个gap, 好放core.img, 制作core.img的时候, 把/boot的分区信息和目录信息写入到core.img里面去了

gpt分区的话 需要有一个标记为bios_grub的分区来放core.img,

安装target分为2种, 一种是i386-pc, 另一种是uefi
