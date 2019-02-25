# 修改服务器端参数

在其中添加一行内容,意思是向客户端每60秒发一次保持连接的信号

ClientAliveInterval  60

如果仍要设置断开时间,还有一个参数可以添加

ClientAliveCountMax  60

意思是如果客户端60次未响应就断开连接,依据你期望的时间来设定

# 修改本地参数

也可以让客户端向服务器发送保持连接信号,路径是/etc/ssh/ssh_config

在其中类似的添加相应的参数也行

ServerAliveInterval  60

ServerAliveCountMax  60

