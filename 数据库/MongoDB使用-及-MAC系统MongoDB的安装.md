>MongoDB是一个跨平台的，面向文档的数据库。由C++语言编写。旨在为WEB应用提供可扩展的高性能数据存储解决方案。

![基本概念.png](http://upload-images.jianshu.io/upload_images/3229842-087655fc2b532f99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###什么是NoSql？
``NoSql``，全称是`` Not Only Sql``,指的是非关系型的数据库。下一代数据库主要解决几个要点：非关系型的、分布式的、开源的、水平可扩展的。原始的目的是为了大规模web应用，这场运动开始于2009年初，通常特性应用如：模式自由、支持简易复制、简单的API、最终的一致性（非ACID）、大容量数据等。NoSQL被我们用得最多的当数``key-value``存储，当然还有其他的文档型的、列存储、图型数据库、xml数据库等。
****

###为什么要使用MongoDB?
JSON风格文件的形式，面向文档存储：数据存储
* 对任何属性可索引
* 复制和高可用性
* 自动分片
* 丰富的查询
* 快速就地更新

****
###MongoDB的特点
它的特点是高性能、易部署、易使用，存储数据非常方便。主要功能特性有：
* 面向集合存储，易存储对象类型的数据。
* 模式自由。
* 支持动态查询。
* 支持完全索引，包含内部对象。
* 支持查询。
* 支持复制和故障恢复。
* 使用高效的二进制数据存储，包括大型对象（如视频等）。
* 自动处理碎片，以支持云计算层次的扩展性。
* 支持RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
* 文件存储格式为BSON（一种JSON的扩展）。
* 可通过网络访问。
****
###何处能使用MongoDB？
* 大数据
* 内容管理和交付
* 移动和社交基础设施
* 用户数据管理
* 数据平台
****
>MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。

######基本的用法是存储JSON数据，这很适合JavaScript程序。其特性如下：
   1. 没有表结构的概念，每条记录可以有完全不同的结构
   2. 业务开发方便快捷
   3. sql数据库需要事先定义表结构再使用




##MAC 系统下载安装 mongodb
   1、MAC MongoDB [下载地址](https://www.mongodb.com/download-center?jmp=nav#community)
   2、下载MongoDB后，将mongodb-osx-x86_64-3.4.5.tar.ge 解压得到mongodb这个文件夹 复制到 /usr/local 路径下。
``默认情况下在Finder中是看不到 /usr 这个目录的（终端用得溜的请略过），可以打开Finder后按shift + command +G 输入 /usr/local后回车便能看到这个隐藏的目录了``

![图示.png](http://upload-images.jianshu.io/upload_images/3229842-be8e3419e957ecf9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3、上图中展示的就是我的本机的目录结构了，在/usr/local/mongodb/bin下就是mongodb的执行文件了。
4、在根目录下新建 data 文件夹，data 文件夹里面创建一个db文件夹，里面是用来存放数据库及其数据。
5、终端切换到/usr/local/mongodb/bin目录下。
6、执行 ./mongod 启动服务端。

![执行 ./mongod后的图示.png](http://upload-images.jianshu.io/upload_images/3229842-aad43baa63a2cd97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
7、 如上图，显示等候客户端连接的界面就代表启动成功了，如果不成功检查下/data/db文件夹的位置是否正确。如果不行，删除重建。
8、打开浏览器，输入localhost:27017,会出现"It looks like you are trying to access MongoDB over HTTP on the native driver port."。
9、重新打开一个终端 进入 /usr/local/mongodb/bin这个目录，执行./mongo 命令，即可连接上。

![屏幕快照 2017-06-23 15.15.11.png](http://upload-images.jianshu.io/upload_images/3229842-23b7361115d30b44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####注意：第六步 和 第九步  输入的执行命令  不相同！
10、如上图所示 ，终端上会一直显示一个 ‘>’ 符号，就代表连接成功了，此时就可以输入mongodb的sql命令：
####demo 是创建的一个集合名字
```
show dbs //显示数据库
use demo //使用某个数据库
db.demo.insert({'name':'demo'}) //插入一条记录
db.demo.find() //查找所有记录
db.demo.findone() //查找一条记录
db.dropDatabase() //删除数据库
db.demo.drop //删除指定集合
show collections //显示所有集合
db.createColletion('demo') //创建集合
db.demo.save({}) //插入记录
db.demo.update({'_id',1},{$set:{name:'demo',age:20}})
db.demo.remove({}) //删除所有集合
for(var i=1;i<=10;i++){db.demo.insert({"name":"king"+i,"age":i})} //循环插入10条记录
db.demo.find().pretty() //格式化显示查询结果
db.demo.find().count() //查询数据条数
db.demo.find({"age":5}) /查找age是5的条目
db.demo.find({“age”:{$gt:5}}) //查找age大于5的条目
db.demo.find({"age":{$gt:5}}).sort({"age":1}) //查找age大于5的条目且升序排列
db.demo.find({"age":{$gt:5}}).sort({"age”:-1}) //查找age大于5的条目且降序排列
```

#####MongoDB 的使用也会有一些限制，例如，它不适合于以下几个地方。
* 高度事务性的系统：例如，银行或会计系统。传统的关系型数据库目前还是更适用于需要大量原子性复杂事务的应用程序。
*  传统的商业智能应用：针对特定问题的BI 数据库会产生高度优化的查询方式。对于此类应用，数据仓库可能是更合适的选择。
*  需要SQL 的问题。
