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
