## [Install Docker Compose](https://docs.docker.com/compose/install/)

# docker-compose安装

## [docker-compose简介](../05、docker技能包/03、docker-compose使用/01、docker-compose简介.md)

## 方法一：

Linux 安装，MAC 和 windows 见上面的链接
```shell script
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
> 如果报 [14660] Cannot open self /usr/local/bin/docker-compose or archive /usr/local/bin/docker-compose.pkg
> 应该是包没下载完整，安装步骤再来一遍。

### 查看版本
```shell script
$ docker-compose version
```
## 方法二：用pip方式安装

确保已经安装好pip

```shell script
#安装docker-compose
$ pip install docker-compose 
#查看版本
$ docker-compose version
```


## [02、Docker-Compose简介安装使用.md](../05、docker技能包/03、docker-compose使用/02、Docker-Compose简介安装使用.md)


## 遇到的问题

### -bash: /usr/local/bin/docker-compose: 权限不够

修改docker-compose命令执行权限：
```shell script
$ sudo chmod +x /usr/local/bin/docker-compose
```

### [14660] Cannot open self /usr/local/bin/docker-compose or archive /usr/local/bin/docker-compose.pkg

> 安装时，curl下载下来的文件是不完整的，而且没有给出任何错误信，

> 可以看到我通过curl下载的文件比使用浏览器下载后又上传到服务器上的文件大小要小.


将文件上传到 /usr/local/bin/ 文件夹下，然后将其重命名为docker-compose，修改此文件的权限，
增加可执行：chmod +x /usr/local/bin/docker-compose

<https://www.cnblogs.com/sixiweb/p/7048914.html>

 






