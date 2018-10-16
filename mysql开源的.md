# 关系型数据库   mysql（开源的）端口为3306

navicat数据库应用链接软件

有条理的，快速的处理数据

向数据库中存入数据：命令行、软件、程序存入数据

### 架构  

c/s架构    依赖于下载客户端

b/s架构    不依赖于客户端，在浏览器中实现

## 命令

### 数据库的基本操作

mysql -hlocalhost(本地的)  -uroot  -p  进入数据库（-h(localhost本地地址)，-u(username用户名)，-p(password密码)）

show databases;  查看里边的库

create database 名字;   创建库

use 库名;   选择用的库

show tables;  查看库中的表

create table stu表名(        **创建表**

id  int(10)   auto_increment(自增)  primary key(主键),

name  varchar(255),

age varchar(10),

sex  varchar(10)

)default charset=utf8;

desc 表名;   查看表的结构

insert into 表名 (name,sex,age) values('张三','男','20')    向表中插入内容

（insert into stu (name,sex,age) values('%s','%s','%s')%(name,sex,age)/insert into stu (name,sex,age) values(%s,%s,%s),(name,sex,age)）

select * from 表名;        查看表的内容

update stu(表名) set sex='女'  where id=1；  更改表的内容

delete from stu(表名) where id=1;    删除表的内容

drop table tablename表名        删除表

drop database 库名;     删除库



pip uninstalled 包名    利用pip下载包

### 创建虚拟环境·：

在终端执行以下口令

python3 -m  venv  abc名字

cd abc名字

cd bin

source ./activate

利用pip下载flask，pymysql等包

#### 步骤

安装pip（官网源码安装）

创建虚拟环境

在终端执行以下口令

python3 -m  venv  abc名字

cd abc名字

cd bin

source ./activate

sudo apt-get install python3.4-venv(安装使python)

升级pip版本pip install -U pip



**退出虚拟环境**：deactivate



**问题：python包的上传**

**虚拟文件的创建**

**客服端的创建**

### ajax(async(异步) javascript and xml(数据))    MDN查看相关知识

**ajax产生的原由**：

​	架构  

​	c/s架构    依赖于下载客户端，更新不及时（不基于网络，操作流畅）

​	b/s架构    不依赖于客户端，在浏览器中实现，可以随时访问最新的内容，免去用户的下载（基于网络，会有					延迟，不能够流畅的操作，体验性不好）

ajax结合了这两点。

**ajax要解决的问题：**

​	1.页面无刷新操作数据

​	2.按需获取的问题

​	3.让基于b/s架构的软件能够同基于c/s架构的软件，操作流畅

var ajax=new XML HttpRequest()    定义ajax对象，让他去进行操作

ajax.onr eadystatechange=function(){     当ajax对象状态发生改变时执行的语句

​	if(ajax.readyState==4)   ajax.readState  1接到要求  2出发  3找到地址 4取到数据

​	if(ajax.state==200)    200--节点任务成功完成

}

```py
ajax.onload=function(){   等同于上面的语句（监听）
  ajax.response   获取的内容
}
```

ajax.open('post/get','2.html')   #到哪调取，以什么方式取    取数据的方式：get、post    open(方式，地址，同步/异步(true/false),服务器的用户名和密码)后两个参数一般不写

ajax.send()  可以去了



### 注意的问题

#### ajax的返回值：

ajax的返回值： document   text  json  blod(二进制)   ....(默认text)          ajax.responseType='document'控制类型

#### ajax中post 与 get传递的区别

post传递数据

​	ajax.open('post','/')

​	ajax.setRequestHeader('content-type','application/x-www-form-urlencoded')   指定内容传递类型

​	ajax.send('name=zhangsan')   在此处传数据

get传递数据

​	ajax.open('get','/?name=zhangsan&sex=nan')  通过地址栏传递  ?+{name:name,age:age}

​	ajax.send( )



#### ajax的封装函数

```py
function ajax(parames) {
        if (typeof (parames)!='object'){
            console.error('参数错误')
            return;
        }
        //参数初始化
        let type = parames.type || 'get'
        let url = parames.url
        if (url==''){
            console.error('输入操作地址')
            return;
        }
        let gettype = parames.gettype || 'text'
        let date = parames.date || ''
        let atr1=''
        if (typeof date=='object'){
            for(let i in date){
                atr1+=i+'='+date[i]+'&'
            }
        }
        date=atr1.slice(0,-1)
        // }else{
        //     date=parames.date
        // }
        let ajax = new XMLHttpRequest()
        ajax.responseType = gettype
        ajax.onload = function () {
            parames.success(ajax.response)


        }
        if (type == 'get') {
                ajax.open(type, url + '?' + date)
                ajax.send()
            } else if (type == 'post') {
                ajax.open(type, url)
                ajax.setRequestHeader('content-type', 'application/x-www-form-urlencoded')
                ajax.send(date)
            }
    }
    引用
    ajax({
       ajax({
        url:'/select',
        gettype:'json',
        success:function(date){     date为获取的结果，也就是response
            for(var i=0;i<date.length;i++){
                let tr=document.createElement('tr')
                let atr=`<td class="aa">${date[i].id}</td><td>${date[i].name}</td><td>${date[i].sex}</td><td>${date[i].age}</td><td class="aa"><button type="submit" class="remove">删除</button></td>`
                tr.innerHTML=atr
                table.childNodes[1].appendChild(tr)
            }
        }
    })
    })
```

向数据库中导入sql文件：source  path(文件位置 )

### 函数

地址、方式、返回的类型、传递的数据、





seo搜索引擎优化



### 业务逻辑（开发方式）

一.放在服务器

- 优点
  - [ ] 业务逻辑清晰
  - [ ] 人的工作量少
  - [ ] 首页加载速度快
- 缺点
  - [ ] 用户体验差
  - [ ] 服务器压力大
  - [ ] 不利于协同工作

二.ajax

-  优点
  - [ ] 用户的体验比较流畅
  - [ ] 减轻服务器的压力
  - [ ] 有利于协同工作
- 缺点
  - [ ] 业务逻辑不清晰
  - [ ] 人的工作量大

三.mvvm  model--模型---数据   view---视图--模板---html和css

​     数据到试图   视图到数据   双向数据绑定

​     框架代表：angular和vue外哦（基于nodejs）