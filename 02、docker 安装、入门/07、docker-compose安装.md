## [Install Docker Compose](https://docs.docker.com/compose/install/)

# docker-compose安装

## [docker-compose简介](../05、docker技能包/03、docker-compose使用/01、docker-compose简介.md)

## 方法一：

Linux 安装，MAC 和 windows 见上面的链接
```shell script
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
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