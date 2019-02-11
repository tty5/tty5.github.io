---
categories: goland
---

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

```
https://colobu.com/2014/12/02/go-socket-programming-TCP/

package main
import (
	"flag"
	"fmt"
	"io"
	"net"
	"os"
)
var host = flag.String("host", "", "host")
var port = flag.String("port", "3333", "port")
func main() {
	flag.Parse()
	var l net.Listener
	var err error
	l, err = net.Listen("tcp", *host+":"+*port)
	if err != nil {
		fmt.Println("Error listening:", err)
		os.Exit(1)
	}
	defer l.Close()
	fmt.Println("Listening on " + *host + ":" + *port)
	for {
		conn, err := l.Accept()
		if err != nil {
			fmt.Println("Error accepting: ", err)
			os.Exit(1)
		}
		//logs an incoming message
		fmt.Printf("Received message %s -> %s \n", conn.RemoteAddr(), conn.LocalAddr())
		// Handle connections in a new goroutine.
		go handleRequest(conn)
	}
}
func handleRequest(conn net.Conn) {
	defer conn.Close()
	for {
		io.Copy(conn, conn)
	}
}

```

```
package main
import (
	"flag"
	"fmt"
	"net"
	"os"
	"strconv"
)
var host = flag.String("host", "localhost", "host")
var port = flag.String("port", "3333", "port")
func main() {
	flag.Parse()
	conn, err := net.Dial("tcp", *host+":"+*port)
	if err != nil {
		fmt.Println("Error connecting:", err)
		os.Exit(1)
	}
	defer conn.Close()
	fmt.Println("Connecting to " + *host + ":" + *port)
	done := make(chan string)
	go handleWrite(conn, done)
	go handleRead(conn, done)
	fmt.Println(<-done)
	fmt.Println(<-done)
}
func handleWrite(conn net.Conn, done chan string) {
	for i := 10; i > 0; i-- {
		_, e := conn.Write([]byte("hello " + strconv.Itoa(i) + "\r\n"))
		if e != nil {
			fmt.Println("Error to send message because of ", e.Error())
			break
		}
	}
	done <- "Sent"
}
func handleRead(conn net.Conn, done chan string) {
	buf := make([]byte, 1024)
	reqLen, err := conn.Read(buf)
	if err != nil {
		fmt.Println("Error to read message because of ", err)
		return
	}
	fmt.Println(string(buf[:reqLen-1]))
	done <- "Read"
}

```
