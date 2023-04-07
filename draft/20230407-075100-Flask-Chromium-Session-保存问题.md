---
title: flask | flask 会话 session
date: 2023-03-22 12:00:00
tags:

---

flask 会话 session，Chromium 浏览器，使用 localhost 访问不能保存成功，使用 127.0.0.1 可以保存成功

<!-- more --> 

环境

Windows10、Python 3.9.7、flask 2.2.2

```python
from flask import Flask, request, current_app, session
from flask_cors import CORS
import os

app = Flask(__name__)
app.secret_key = os.urandom(24)


@app.route('/', methods=["GET", 'POST'])
def hello_world():
    return "Hello World"


@app.route('/signIn', methods=["GET", 'POST'])
def sign_in():
    """登录"""
    session["isLogin"] = True
    session["userMsg"] = {
        "account": "example"
    }
    return "登录成功"


@app.route('/signOut', methods=["GET", 'POST'])
def sign_out():
    """退出登录"""
    session.pop('isLogin', None)
    session.pop('userMsg', None)
    return "退出登录"


@app.route('/user_msg', methods=['POST', "GET"])
def user_msg():
    if session.get("isLogin") is not None:
        return session["userMsg"]
    else:
        return "None"


@app.before_request
def before():
    """
    针对app实例定义全局拦截器
    """
    url = request.path  # 读取到当前接口的地址
    app = current_app._get_current_object()
    with app.app_context():
        print(url, session)


CORS(app, supports_credentials=True)

if __name__ == '__main__':
    app.run(port=5000)
```



## 问题概述

