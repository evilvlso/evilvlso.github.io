### 使用
```
uwsgi --ini uwsgi.ini             # 启动
uwsgi --reload uwsgi.pid          # 重启
uwsgi --stop uwsgi.pid            # 关闭
```
<!--more-->
### 配置
```
[uwsgi]
chdir=/opt/   

callable=app  #flask专用
home=/root/env/
wsgi-file=xdbg/wsgi.py
master=true
py-autoreload=1                              # py文件修改，自动加载
processes=4
threads=2

pidfile=%(chdir)/uwsgi.pid
socket=/socket/uwsgi.sock
chmod-socket = 664
vacuum=true    #退出uwsgi是否清理中间文件，包含pid、sock和status文件
daemonize=%(chdir)/cloudmonitor.log  #配合supervisor去掉并且改到stdout_logfile docker中要去掉
static-map = /static=/opt/static
```

> 参考 https://www.jianshu.com/p/c3b13b5ad3d7