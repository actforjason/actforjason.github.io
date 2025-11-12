# Python虚拟环境 Pip Install TLS SSL WARNING

Python 虚拟环境 WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.
<!--more-->
如果使用的是Conda创建的venv，需要在**Conda Prompt**中运行pip install命令。
否则使用单纯的Python解释器创建虚拟环境，就可以避免错误。

虚拟环境中设置http代理：
```python
pip config set global.proxy http://{host}:{port}

output:

Writing to C:\Users\{username}\AppData\Roaming\pip\pip.ini
```

参考问题：
[Can't install any package via `pip` on windows 10, ssl module in Python is not available · Issue #1139 · pypa/virtualenv](https://github.com/pypa/virtualenv/issues/1139)


---

> 作者: [Jason](https://github.com/actforjason)  
> URL: https://actforjason.github.io/posts/%E7%96%91%E9%9A%BE%E6%9D%82%E7%97%87/python%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83-pip-install-tls-ssl-warning/  

