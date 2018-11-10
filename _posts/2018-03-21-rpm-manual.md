# rpm

查看所有安装的rpm包 rpm -qa

查看一个包是否安装 rpm -q package

查看一个已安装包里面的文件 rpm -ql package

查看一个具体包里面的文件 rpm -qlp package

查看一个文件属于哪个包 rpm -qf file-path

查看远程的包，yum search

查看远程包包含哪些文件 repoquery -ql package

查找远程的文件在哪个包里面 repoquery -qf filepath yum provides filepath

查看远程yum源列表 yum repolist

查看有个rpm包有多少候选项 yum list kernel

# yum

检查更新 yum check-upate

更新某个软件 yum update glibc

查看一个包的安装源 yum list glibc

列出所有的源 yum repolist

列出所有的软件包 yum list

临时enbale一个repo yum --enablerepo google-chrome list

临时enable所有的repo yum --enablerepo=* repolist

enable disable一个repo, 去repo file文件夹里面改
