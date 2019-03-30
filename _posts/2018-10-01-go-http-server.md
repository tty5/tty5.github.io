# go 函数指针
go的函数指针可以用结构体的成员函数来做初始化, 自然要使用一个对象的函数指针

# go http server 服务端
```
func myHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello there!\n")
}

http.HandleFunc("/", myHandler)
log.Fatal(http.ListenAndServe(":8080", nil))
```

# go http client 客户端
```
    response, err := http.Get("http://www.baidu.com")
    defer response.Body.Close()
    body, _ := ioutil.ReadAll(response.Body)

    另一种
    http.client.do(req)

    client可以有很多参数
    req内容可以随意组装

    // req
    req, err := http.NewRequest("GET", "http://vt1.doubanio.com/201706150839/fd34356de8a03bb99869924284b0ef46/view/movie/F/302160401.flv", nil)

    var netTransport = &http.Transport{
        Dial: (&net.Dialer{
            Timeout:   10 * time.Second,
            KeepAlive: 30 * time.Second,
        }).Dial,
        TLSHandshakeTimeout:   5 * time.Second,
        ResponseHeaderTimeout: 10 * time.Second,
        ExpectContinueTimeout: 1 * time.Second,
    }
    var netClient = &http.Client{
        Timeout:   time.Second * 30,
        Transport: netTransport,
    }

    // get
    response, _ := netClient.Get("http://www.golangnote.com/")
    
```

# go http client 记录
http.Client.Do是通用的做法, 里面的成员变量Transport控制tcp连接的具体行为

### 获取conn
```
0 net/http.(*Transport).getConn
1 net/http.(*Transport).roundTrip
2 net/http.(*Transport).RoundTrip
3 net/http.send
4 net/http.(*Client).send
5 net/http.(*Client).do
6 net/http.(*Client).Do
7 main.main
8 runtime.main
9 runtime.goexit
```

### 根据域名获得ip
```
0  net.(*Resolver).lookupIPAddr
1  net.(*Resolver).internetAddrList
2  net.(*Resolver).resolveAddrList
3  net.(*Dialer).DialContext
4  net.(*Dialer).Dial
5  net.(*Dialer).Dial-fm
6  net/http.(*Transport).dial
7  net/http.(*Transport).dialConn
8  net/http.(*Transport).getConn.func4
9  runtime.goexit
```

### 解析dns
```
0 net.(*Dialer).DialContext
1 net.(*Resolver).dial
2 net.(*Resolver).exchange
3 net.(*Resolver).tryOneName
4 net.(*Resolver).goLookupIPCNAMEOrder.func1
5 runtime.goexit
```

