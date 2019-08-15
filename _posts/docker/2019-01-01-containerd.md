# 安装crictl和containerd
### 安装containerd
curl -s https://lxx-sh.oss-cn-shanghai.aliyuncs.com/containerd -o /usr/bin/containerd; chmod 755 /usr/bin/containerd

### 安装crictl
curl -s https://lxx-sh.oss-cn-shanghai.aliyuncs.com/crictl -o /usr/bin/crictl; chmod 755 /usr/bin/crictl
### crictl yaml
```
cat <<EOF > /etc/crictl.yaml
runtime-endpoint: unix:///run/containerd/containerd.sock
image-endpoint: unix:///run/containerd/containerd.sock
timeout: 10
debug: false
EOF
```
