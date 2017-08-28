以发布一个``iam-sun-iam-moon``的``package``到``npm``为例; 
### 1、首先需要安装node和npm
### 2、编写模块
一个最简单的NPM包由主模块``index.js``和包描述文件``package.json``组成。
#### 第一步
在项目的根目录下创建一个名字为``node_modules``的目录，此目录用来放置所有的``node``模块。
#### 第二步
在``node_modules``目录下创建一个名字为``iam-sun-iam-moon``目录。
#### 第三步
``iam-sun-iam-moon``目录下新建两个文件：

* index.js:

```javascript
function iam-sun-iam-moon() {
  console.log("There is the iam-sun-iam-moon.");//主要代码
}
module.exports = iam-sun-iam-moon;
```

* package.json:
这个文件包含了module的所有信息，比如名称、版本、描述、依赖、作者、license等。
执行``npm init``，系统会提示你输入所需的信息，不想输入的直接输入Enter可以跳过。

```
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (iam-sun-iam-moon)
version: (1.0.0)
description:
entry point: (index.js)
test command:
git repository:
keywords:
author: xinyu
license: (ISC)
About to write to /Users/yu/Desktop/iam-sun-iam-moon/package.json:

{
  "name": "iam-sun-iam-moon",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "xinyu",
  "license": "ISC",
  "description": ""
}
Is this ok? (yes)
```
输入完成之后，系统会要你确认文件的内容是否有误，如果没有问题直接输入yes或者按enter，这样package.json就创建好了。

### Package.json 属性说明
<br>name - 包名。
<br>version - 包的版本号。
<br>description - 包的描述。
<br>homepage - 包的官网 url 。
<br>author - 包的作者姓名。
<br>contributors - 包的其他贡献者姓名。
<br>dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
<br>repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
<br>main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
<br>keywords - 关键字

### 发布
* 首先要注册一个[npm账号](https://www.npmjs.com/signup)
* 更改``.npmrc  `` 中的配置为：
```
registry = http://registry.npmjs.org/.
```    
* 为了维护包，npm必须要使用仓库账号才允许将包发布到仓库中。
注册账号的命令是``npm adduser``，按照提示填写相关信息即可。 

 ![](http://upload-images.jianshu.io/upload_images/3229842-54eebe0838928fee.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 上传包，命令是 ``npm publish``
* 上传完成后我们就可以在官方仓库中查看我们刚刚写的包了[https://www.npmjs.org/](https://www.npmjs.org/)

### 使用
在需要使用的文件夹目录下输入指令``npm install iam-sun-iam-moon``就可以把需要的npm包下载下来使用了。

创建测试实例，创建``test``目录，里面创建文件 ``test.js``

test.js
```
var test = require('iam-sun-iam-moon');
test();
```

命令行进入test目录，输入命令``node test.js``,输出``There is the iam-sun-iam-moon !``。

### 常见问题
* 更新包的话，修改代码后不能直接发布，这里我们需要修改``package``的``version``号，修改之前先说下``npm``维护``package``版本的规则``x.y.z``

  >x: 主版本号,通常有重大改变或者达到里程碑才改变;
  <br>y: 次要版本号,或二级版本号,在保证主体功能基本不变的情况下,如果适当增加了新功能可以更新此版本号;
  <br>z: 尾版本号或者补丁号,一些小范围的修修补补就可以更新补丁号.

  ```
   $ npm version patch <=> z++
   $ npm version minor <=> y++ && z=0
   $ npm version major <=> x+= && y=0 && z=0
  ```
   然后执行``npm publish``就可以更新到``npm``了
   
* 如果在发布中显示类似'请确认你是否有权限更新xxx包'的英文提示，这就说明你的包名有人使用了，应该换一个名字。


* 删除发布的模块

 ```
  $ npm unpublish package@version
  或者
  $ npm unpublish --force package
```
