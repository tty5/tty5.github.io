---
categories: linux-cmd
---

# install

## centos
yum install epel-release -y

## fedora
yum install cmake dstat pixman-devel glib2-devel psmisc strace sysstat ctags jq make git procps-ng vim less wget unzip bash-completion openssh-clients openssh-server iproute iputils gcc gdb net-tools autoconf automake libevent-devel ncurses-devel python2-pip -y

yum install bind-utils ltrace nmap traceroute pciutils openssl man rpmdevtools elfutils-libelf-devel openssl-devel bc rpm-build flex bison -y

yum install whois perl-podlators texinfo libcap-devel libattr-devel libcap-ng-devel numactl-devel libuuid-devel libpng-devel cyrus-sasl-devel libtool acpica-tools libstoraged-devel lz4-devel libaio-devel btrfs-progs-devel libseccomp-devel -y

pip install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
