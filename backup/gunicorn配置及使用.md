### 常用操作

启动:
`gunicorn -c config.py app:app`

停止:`ps aux | grep "gunicorn"|grep -v "grep"|awk -F " " '{print $2}| xargs -i kill -9 {}'`

**awk grep kill** 配合着来，有些粗鲁
<!--more-->

### 配置(配置文件可是py文件)

```
import multiprocessing
import os
base = os.path.abspath(os.path.dirname(__file__))
workers = multiprocessing.cpu_count() * 2 + 1
threads = 6
reload = 0.   # debug模式
bind = '0.0.0.0:9999'
daemon = 'false'     #docker中要关闭
worker_class = "gevent"    #
worker_connections = 2000
loglevel = 'error'
accesslog = os.path.join(base,"gunicorn_acess.log")
errorlog = os.path.join(base,"gunicorn_error.log")
max_requests=300
```