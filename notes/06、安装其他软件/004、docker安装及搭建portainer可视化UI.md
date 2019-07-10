
## [原文](https://www.jianshu.com/p/fbff35bea72d)

# docker安装及搭建portainer可视化UI

## 安装portainer可视化UI

1、拉取portainer镜像，

执行：
```docker
docker pull portainer/portainer

```
如果出现如下错误：

```
Using default tag: latest

Error response from daemon: Get https://registry-1.docker.io/v2/: dial tcp: lookup registry-1.docker.io on [::1]:53: read udp [::1]:51728->[::1]:53: read: connection refused

```
解决办法：需要配置Linux系统dns地址，修改文件vim /etc/resolv.conf

配置如下内容：

```
nameserver 8.8.8.8

nameserver 114.114.114.114

```
然后保存退出即可

portainer镜像拉取成功，如图所示：

也可以通过镜像查询命令docker images来查看刚才下载的镜像

2、运行portainer镜像，执行：

```docker
docker run -d -p 9000:9000 \

--restart=always \

-v /var/run/docker.sock:/var/run/docker.sock \

--name prtainer \

portainer/portainer

```


## 访问portainer服务

打开浏览器，输入服务器的IP或域名+端口号（9000），

demo：http://127.0.0.1:9000/

首次访问会进入初始化用户配置页面，相关设置如下：


设置密码

选择本地


到这里，可视化docker管理界面已经搭建好了



