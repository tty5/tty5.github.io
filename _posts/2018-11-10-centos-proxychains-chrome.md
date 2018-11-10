# centos 安装 proxychains

```rpm -Uvh https://mirrors.aliyun.com/fedora/releases/27/Everything/x86_64/os/Packages/p/proxychains-ng-4.11-4.fc27.x86_64.rpm```

# chrome

```
cd /ect/yum.repos.d/
vim google-chrome.repo

[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
enabled=0
gpgcheck=1
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub

yum --enablerepo google-chrome -y install google-chrome-stable
```
