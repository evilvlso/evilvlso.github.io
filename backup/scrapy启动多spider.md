### 好使
```Python
import scrapy
from scrapy.crawler import CrawlerProcess
from scrapy.utils.project import get_project_settings
process = CrawlerProcess(get_project_settings())
# 指定多个spider
process.crawl("fen")
process.crawl("fuck")
# 执行所有 spider
# for spider_name in process.spider_loader.list():
#     print(spider_name)
    # process.crawl(spider_name)
process.start()

```