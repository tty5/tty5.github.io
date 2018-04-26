# install

yum install kexec-tools crash yum-utils -y

systemctl status kdump

systemctl start kdump

vmcore路径在/etc/kdump.conf文件里面

