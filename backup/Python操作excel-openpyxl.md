> openpyxl是一个很好用的操作excel的库
> 
> 常用的操作：
> 
>  * 添加表头 **add_sheet**
>  * 添加数据(元组) **add_data**
>  * 设置表头格式(仅字体)  **set_header_font**
>  * 删除 **sheet delete_sheet**
>  * 保存excel **save**
> 
> 还有很多友好的操作

```Python
class Xlsx():
    def __init__(self):
        self.workbook = Workbook()
        self.index=1
        pass

    def add_sheet(self,sheetname="Sheet"):
        return self.workbook.create_sheet(sheetname,self.index+1)

    def add_data(self,data,sheet="Sheet"):
        '''
        :param sheet :sheet对象
        :param data: data最好是一个元组
        :return:
        '''
        if isinstance(data,tuple):
            sheet.append(data)
        else:
            sheet.append(tuple(data))

    def set_header_font(self,sheetname="Sheet"):
        '''
        格式化行头
        :param sheetname:
        :return:
        '''
        font = Font(u'宋体', size=13, bold=True, color='000000')
        for i in sheetname["1"]:
            i.font = font
            
    def delete_sheet(self,sheetname="Sheet"):
        '''
        删除sheet
        :param sheetname:
        :return:
        '''
        self.workbook.remove(self.workbook[sheetname])

    def save(self,filename):
        self.workbook.save(filename)
```