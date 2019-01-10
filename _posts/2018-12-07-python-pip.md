# python aliyun mirror
```
pip install --upgrade pip  -i https://mirrors.aliyun.com/pypi/simple
```

# qh
## 临时使用
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```

## 设为默认
升级 pip 到最新的版本 (>=10.0.0) 后进行配置
```
pip install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
