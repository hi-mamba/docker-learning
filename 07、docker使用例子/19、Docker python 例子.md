

# Docker python 例子

在 ~/python/myapp 目录下创建一个 helloworld.py 文件，代码如下：
```python
#!/usr/bin/python

print("Hello, World!");
```
运行容器

```shell script
[root@localhost py-docker]# docker run -v $PWD/myapp:/usr/src/myapp -w /usr/src/myapp python:latest python helloworld.py
hello docker world
```
命令说明：

-v $PWD/myapp:/usr/src/myapp: 将主机中当前目录下的 myapp 挂载到容器的 /usr/src/myapp。

-w /usr/src/myapp: 指定容器的 /usr/src/myapp 目录为工作目录。

python helloworld.py: 使用容器的 python 命令来执行工作目录中的 helloworld.py 文件。






