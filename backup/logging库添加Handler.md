### logging常用配置
```Python
    logger = logging.getLogger('what')
    logger.setLevel(logging.INFO)
    #设置日志格式
    formater=logging.Formatter(fmt='%(name)s %(asctime)s %(filename)s [line:%(lineno)d] %(levelname)s : %(message)s ',datefmt='%Y/%m/%d %H:%M')
    #文件Handler
    fh=logging.FileHandler('test.log','a',encoding='utf-8')
    fh.setLevel(logging.ERROR)
    fh.setFormatter(formater)
    #自定义Handler
    th=CustomHandler()
    th.setFormatter(formater)
    th.setLevel(logging.INFO)
    #终端Handler
    ch = logging.StreamHandler()
    ch.setLevel(logging.INFO)
    ch.setFormatter(formater)
    #添加Handler
    logger.addHandler(fh)
    logger.addHandler(ch)
    logger.addHandler(th)
```
### 自定义Hander
```Python
class CHandler(logging.Handler):
    def __init__(self):
        logging.Handler.__init__(self)
        self.client=pymysql.Connection(host='127.0.0.1',user='root',passwd='qweqwe',db='sharesnews',charset='utf8mb4',autocommit=True)
        self.cursor=self.client.cursor()
    def emit(self, record):
        try:
            sql='insert into exceptions (exception,add_time) VALUES (%s,%s)'
            msg = sql.format(record)
            self.cursor.execute(sql,(msg,datetime.now()))
        except Exception:
            self.handleError(record)
            self.client.rollback()
```