---
title: 【转】【译】flask 框架配置基础的 URL（baseURL）
date: 2023-01-23 20:13:00
tags:

---

flask 框架配置基础的 URL（baseURL）

<!-- more --> 

 之前使用 Python 的 **flask** 写了一个简单的应用，想要为后端所有的路由配置一个共同的 URL 前缀（如 /api ）。

在 [stackoverflow](https://stackoverflow.com/questions/18967441/add-a-prefix-to-all-flask-routes) 上找到了一些解决方案，这里做一个整理和翻译

## 方法1 - 字符串拼接

```python
from flask import Flask

PREFIX = "/abc/123"

# /abc/123/
@app.route(PREFIX + "/")
def index_page():
  return "This is a website about burritos1"

# /abc/123/about
@app.route(PREFIX + "/about")
def about_page():
  return "This is a website about burritos2"

if __name__ == "__main__":
    app.run(debug='True', port=4444)
```

## 方法2 - Blueprint

```python
from flask import Flask, Blueprint

bp = Blueprint('burritos', __name__,
                        template_folder='templates')

@bp.route("/")
def index_page():
  return "This is a website about burritos1"

@bp.route("/about")
def about_page():
  return "This is a website about burritos2"

app = Flask(__name__)
app.register_blueprint(bp, url_prefix='/abc/123')

if __name__ == "__main__":
    app.run(debug='True', port=4444)
```

## 方法3-

等等

## 参考连接

- [stackoverflow.com - add-a-prefix-to-all-flask-routes](https://stackoverflow.com/questions/18967441/add-a-prefix-to-all-flask-routes)