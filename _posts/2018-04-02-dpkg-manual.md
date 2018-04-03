# dpkg



操作deb 使用dpkg 命令工具， dpkg 是Debian package的简写。 下面列举常用的 操作：

dpkg –I name.deb  查看 包的详细信息（其中的I为大写的i）；  （—info)

dpkg –c name.deb  查看 包的内容；  （—contents)

dpkg –i name.deb  安装一个 deb 包；     (--install),如果出现缺少依赖，可以运行 sudo apt-get -f install ,它可以修复依赖，而dpkg不会自动下载依赖的;（后面提到）

dpkg –r name       删除一个 deb 包，但保留其配置；   (--remove)

dpkg –P name       删除一个 deb 包，包括保留其配置；    (--purge)

dpkg –l name        简单列出包的相关信息；       （—list)

dpkg –L name        列出安装的包的相关文件；     (—listfiles)

dpkg –s name       列出包的相关细节信息；

它的参数有很多，如果需要可以通过 –help来查看；

# apt

sudo apt-get install package-name  ：安装包；

如果要移除软件你则需要使用以下命令:

sudo apt-get remove package-name

但是移除软件并不能将软件包及其配置文件删除,要删除这些需要使用下面的命令:

sudo apt-get purge package-name

要搜索软件包可以使用以下命令:

sudo apt-cache search package-name

apt-cache show package-name   显示包的相关信息，例如描述、版本、大小、依赖以及冲突。

现在你已经知道如何安装和删除软件包,下面的命令可以让你获取最新的软件包套件资讯；在你更改了/etc/apt/sources.list 后需要运行这个命令以令改动生效。

sudo apt-get update

然后您可以用  更新所有有新版本的套件：

sudo apt-get upgrade

apt-get autoclean  如果你的硬盘空间不大的话，可以定期运行这个程序，将已经删除了的软件包的.deb安装文件从硬盘中删除掉。

apt-get clean      类似上面的命令，但它删除包缓存中的所有包。当然多数情况下这些包没什么用了，因此这是个为硬盘腾地方的好办法,包的缓存路径为 /var/cache/apt/archives

apt-get -f install   在Linux中使用命令 apt-get install 或 dpkg -i 时有时候会出现依赖错误， 此时，紧接着执行：apt-get -f install 即可. -f的作用用于修复依赖损坏处，-f ,fix broken;

另外，软件的更新源在 /etc/apt/sources.list内，我们可以修改它，用于更改更新源；
