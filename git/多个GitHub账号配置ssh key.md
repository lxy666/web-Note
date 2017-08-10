### 生成并添加第一个ssh key
```
$ ssh-keygen -t rsa -C "youremail1@xxx.com"
```
在Git Bash中执行命令一路回车，会在~/.ssh/目录下生成id_rsa和id_rsa.pub两个文件
用文本编辑器打开id_rsa.pub，在Github中添加SSH Keys。
### 生成并添加第二个ssh key
```
$ ssh-keygen -t rsa -C "youremail2@xxx.com"
```
这次不能一路回车，给这个文件起一个名字 不然默认的话就覆盖了之前生成的第一个。


![图示](http://upload-images.jianshu.io/upload_images/3229842-4bf6f00e8e57c0b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 目录结构
```
id_ras
id_ras.pub
my
my.pub
```

如果生成的第二个 ssh key 不在~/.ssh/目录下,可以移动到此目录。

### 在~/.ssh/下创建config文件 

```
Host github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa  
  
Host my.github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/my  
```
### 测试正确性
```
ssh -T git@github.com
ssh -T git@my.github.com
```
如果出现Hi xxx!You've successfully authenticated 就说明连接成功了

