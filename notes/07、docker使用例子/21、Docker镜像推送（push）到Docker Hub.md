## [原文](https://blog.csdn.net/boonya/article/details/74906927)

# Docker镜像推送（push）到Docker Hub

## Docker hub注册用户
到官网注册账号：https://hub.docker.com/

在本地Linux登录docker：
```shell script
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: kobe
Password:
Authenticating with existing credentials...
Login Succeeded
```
这里需要注意用户名不能使用邮箱，参考这里

[Unable to docker login through CLI - unauthorized: incorrect username or password](https://github.com/docker/hub-feedback/issues/935)

[【Docker】unauthorized: incorrect username or password](https://www.cnblogs.com/jaxer/p/7742186.html)

docker id 就是你登陆docker web 页面显示的那个名字.

## tag修改镜像名称

推送镜像的规范是：
 
> docker push 注册用户名/镜像名
 
tag命令修改为规范的镜像：
```shell script
$ docker tag java-docker-example kobe/java-docker-example
```

查看修改后的规范镜像：
```shell script
$ docker images;
REPOSITORY                                 TAG                 IMAGE ID            CREATED             SIZE
kobe/java-docker-example                   latest              b4a953adf3bb        About an hour ago   105MB
tensorflow/tensorflow                      nightly-jupyter     dd24fbcec098        6 weeks ago         1.28GB
```

## 推送镜像到Docker Hub

通过push命令推送镜像：

```shell script
$ docker push kobe/java-docker-example
The push refers to repository [docker.io/kobe/java-docker-example]
a729d3305d3f: Pushed
209791487736: Pushed
4dfcdc513358: Pushed
ceaf9e1ebef5: Pushed
9b9b7f3d56a0: Pushed
f1b5933fe4b5: Pushed
latest: digest: sha256:04c7b01fe83b509e2572fcf7102146f73c0f76d8b75a96536f762ddd5c60e565 size: 1569
```

注：推送Docker Hub速度很慢，耐心等待，很有可能失败，失败会尝试多次重传，
之后断开推送（但已推送上去的会保留，保留时间不知道是多久）。

下面是上传完毕的输出（多次重传）：

## 访问Docker Hub发布镜像
https://cloud.docker.com/repository/list

## Docker 使用发布的镜像
因为我们已经发布自己的镜像，以后都可以直接使用docker pull命令拉取使用镜像：

```shell script
$ docker pull kobe/java-docker-example
```