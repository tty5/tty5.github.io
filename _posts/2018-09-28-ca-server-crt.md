# 做个ca的证书, server证书的时候, CN要换一下

1.创建 CA 私钥

```$openssl genrsa -out ca.key 2048```

私钥生成公钥

```openssl rsa -in x.key -pubout > x.pub ```

2.生成 CA 的自签名证书

```
$ openssl req -subj "/CN=Server CA" -new -x509 -days 3650 -key ca.key -out ca.crt
```

查看ca证书内容

```openssl x509 -in ca.crt -noout -text```

3.生成需要颁发证书的私钥

```$ openssl genrsa -out server.key 2048```

4.生成要颁发证书的证书签名请求, CN就是域名, 和上面ca的CN不要一样

```$ openssl req -subj "CN=x.x" -new -key server.key -out server.csr```

5.用 2 创建的 CA 证书给 4 生成的 签名请求 进行签名

```$ openssl x509 -req -days 3650 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt```

如果需要增加ip的, 加上这个san

```-extfile <(printf "subjectAltName=IP:8.8.8.8")```

# 添加ca.crt到系统

添加内容到文件/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem

或者

```
Add	

Install the ca-certificates package: yum install ca-certificates

Enable the dynamic CA configuration feature: update-ca-trust force-enable

Add it as a new file to /etc/pki/ca-trust/source/anchors/: cp foo.crt /etc/pki/ca-trust/source/anchors/

Use command: update-ca-trust extract
```
