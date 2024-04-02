---
* ### 方法一(scrapy适用)
```Python
from scrapy.http.cookies import CookieJar
cookie_jar = CookieJar()
cookie_jar.extract_cookies(response, response.request)
for i in self.cookie_jar:
    p = re.compile(r'<Cookie (.*?) for .*?>')            
    cookies = re.findall(p, str(i))            
    cookies = (cookie.split('=', 1) for cookie in cookies)
    cookies = dict(cookies)
```


* ### 方法二（普适用）
```Python
def get_cookies(response):
    my_cookies = dict()
    # 请求包里带的Cookie
    for cookie in response.request.headers.getlist('Cookie'):
        for ck in cookie.decode('utf8').split(';'):
            try:
                my_cookies[ck.split('=')[0].strip()] = ck.split('=')[1].strip()
            except:
                my_cookies[ck.split('=')[0].strip()] = ''
    # 响应包里给的Set-Cookie
    for cookie in response.headers.getlist('Set-Cookie'):
        for ck in cookie.decode('utf8').split(';'):
            try:
                my_cookies[ck.split('=')[0].strip()] = ck.split('=')[1].strip()
            except:
                my_cookies[ck.split('=')[0].strip()] = ''
    return my_cookies
```