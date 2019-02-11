---
categories: linux-cmd
---

# 配置
```
docker run -it  --network host fedora bash

dnf install -y bash-completion which rinetd vim procps-ng -y
exec bash
vim /etc/rinetd.conf
rinetd
ctrl p q
```
