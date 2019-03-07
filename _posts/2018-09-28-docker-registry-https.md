# 建一个docker registry
```docker run --net host -d registry```

# 建一个https的nginx反向代理

```docker run  --net host -d -v /root/certs:/root/certs -v /root/nginx.conf:/etc/nginx/nginx.conf  nginx```

certs文件夹放服务器公钥和私钥

```
cat nginx.conf

events {
  worker_connections  4096;  ## Default: 1024
}

http {
        server {
            listen       443 ssl;
            ssl_certificate      /root/certs/server.crt;
            ssl_certificate_key  /root/certs/server.key;

            ssl_session_timeout  5m;

            location / {
                proxy_pass http://localhost:5000;
            }
        }
}
```


# docker bash

env TERM=xterm bash -l

