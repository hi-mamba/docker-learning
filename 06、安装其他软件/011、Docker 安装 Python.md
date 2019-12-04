## [Docker 安装 Python](https://www.runoob.com/docker/docker-install-python.html)

# Docker 安装 Python

## 方法一、docker pull python:3.5

查找 Docker Hub 上的 Python 官方镜像
<https://hub.docker.com/_/python?tab=tags>

安装最新
```shell script
docker pull python
```

查看镜像

```shell script
docker images
```

## 方法二、通过 Dockerfile 构建

通过 Dockerfile 创建一个python镜像


