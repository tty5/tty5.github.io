# 没有类, 直接写函数
```
def test_displayEmployee():
    print "test_displayEmployee"
    return True


def test_displayEmployeexx():
    print "test_displayEmployeexx"
    return True
```
```
nosetests -s -v 4.py 
4.test_displayEmployee ... 
test_displayEmployee
ok
4.test_displayEmployeexx ... 
test_displayEmployeexx
ok

```

# 使用类的
```
import unittest

class rbb(unittest.TestCase):

    def setUp(self):
        print ("TestUM:setup() before each test method")

    def tearDown(self):
        print ("TestUM:teardown() after each test method")

    def test_1(self):
        print "test_1"
        return True

    def test_2(self):
        print "test_2"
        return True

```

```
nosetests  -v 3.py
-s 打印出脚本日志
```
