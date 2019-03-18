---
categories: linux-cmd
---

# install

## centos
yum install epel-release -y

## fedora
yum install psmisc strace sysstat ctags jq make git procps-ng vim less wget unzip bash-completion openssh-clients openssh-server iproute iputils gcc gdb net-tools autoconf automake libevent-devel ncurses-devel python2-pip -y

yum install traceroute pciutils openssl man rpmdevtools elfutils-libelf-devel openssl-devel bc rpm-build flex bison -y

yum install btrfs-progs-devel libseccomp-devel -y

pip install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
