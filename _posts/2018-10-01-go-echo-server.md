# go tcp连接服务端

https://github.com/golergka/go-tcp-echo/blob/master/go-tcp-echo.go

```
	l, err := net.Listen("tcp", ":" + strconv.Itoa(*port))
		conn, err := l.Accept()
		size, err := conn.Read(buf)
		conn.Write(data)
```

# 客户端

```
	conn, err := net.Dial("tcp", *host+":"+*port)
	_, e := conn.Write([]byte("hello " + strconv.Itoa(i) + "\r\n"))
	_, e := conn.Write([]byte("hello " + strconv.Itoa(i) + "\r\n"))

```
