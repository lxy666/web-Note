>有时候在学习一些前端框架或前端库时，需要有一个Web服务器作为后端提供数据。如果使用Apache或Tomcat等服务器比较麻烦（需要把代码放到指定位置），而且不够轻量级——相比起使用Python来说。

* 如果没有安装Python的话，需要先安装Python，建议安装Python 3以上的版本。
* 进入你的项目文件夹，打开一个终端（控制台窗口），输入：
```
python -m http.server 8000
```
* 通过 [http://localhost:8000](http://www.voidcn.com/link?url=http://localhost:8000) 就可以在浏览器访问了

* 如果使用的是Python 2，输入：
```
python -m SimpleHttpServer 8000
```
如果系统是``windows``的话，可以将指令写到``cmd``或``bat``脚本中，每次只需要双击脚本就行；
如果系统是``Linux``的话写到脚本中后，记得改文件的执行权限，另外，可以加上 & 实现后台运行。
