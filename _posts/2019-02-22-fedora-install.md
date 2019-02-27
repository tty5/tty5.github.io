---
categories: linux-cmd
---

# install

## centos
yum install epel-release -y

yum install make git procps-ng vim less wget unzip bash-completion openssh-clients iproute iputils gcc gdb net-tools python2-pip -y

pip install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
