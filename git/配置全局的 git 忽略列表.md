1. 先检查一下是否已经有 core.excludesfile 设置:

   git config --get core.excludesfile

2. 如果已有设置，则在原来的配置文件中修改；

    如果还没有设置，则创建一个配置文件：

3. git config --global core.excludesfile '~/.gitignore'

4. 修改配置文件 (~/.gitignore)，加入要忽略的文件。

例如：

```
# 忽略的文件

node_modules

npm-debug.log
```



