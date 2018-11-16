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

```
yum常用命令
1.列出所有可更新的软件清单命令：yum check-update
2.更新所有软件命令：yum update
3.仅安装指定的软件命令：yum install <package_name>
4.仅更新指定的软件命令：yum update <package_name>
5.列出所有可安裝的软件清单命令：yum list
6.删除软件包命令：yum remove <package_name>
7.查找软件包 命令：yum search <keyword>
8.清除缓存命令:
yum clean packages: 清除缓存目录下的软件包
yum clean headers: 清除缓存目录下的 headers
yum clean oldheaders: 清除缓存目录下旧的 headers
yum clean, yum clean all (= yum clean packages; yum clean oldheaders) :清除缓存目录下的软件包及旧的headers

```
# 查看rpm repo url

查看repo的url, 直接看文件就可以了

查看rpm的url, 直接看
```
Use yumdownloader. It's in the yum-utils package.

To get URLs for packages:
查看url
yumdownloader --urls mariadb-server
To actually download a package and all its dependencies:

下载依赖和自己
yumdownloader --resolve mariadb-server
You don't really need aria2 at all
```
