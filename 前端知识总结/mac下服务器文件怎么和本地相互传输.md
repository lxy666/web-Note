如果要是将本地的文件上传到服务器，那么久需要进入本地的文件夹，然后写命令“scp  要上传的文件名称    用户名@主机名：上传到的路径“，点击回车。

如果是从服务器上下载文件，那么要写的命令为“scp -r  用户名@主机名：要下载的文见路径   要保存的位置”，回车。

git 
git init
git remote add origin git@github.com:lxy666/Flak-box-barrage.git
git add .
git commit -m "first commit"
git push origin master
