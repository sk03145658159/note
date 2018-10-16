#### 利用python读写excel文件：xlwt和xlrd

#### 查询http的一些相关请求/转义/常见端口....（搜索http content-type）

#### 获取表单的值： let values=$('form').serializeArray()



### python中实现文件的下载，利用flask中的make_response和send_from_directory

##### python中的make_response模块：自理解将模板转成一个可操作的对象，设置类似cookies信息

##### python中的send_from_directory模块:首选在application下建立一个upload目录，构造upload目录的绝对路径。#然后通过浏览器输入指定文件的文件名来下载。

```py
res=make_response(send_from_directory('.','demo.xls',as_attachment=True))
res.headers['content-disposition']='attachment;filename=1.xls'
return res
```

