


# docker 安装及其卸载

- docker-io, docker-engin 是以前早期的版本，版本号是 1.*，默认centos7 安装的是docker-io，最新版是 1.13。

- docker-ce 是社区版本，适用于刚刚开始docker 和开发基于docker研发的应用开发者或者小型团队

- docker-ee 是docker的企业版

## 安装Docker

### ubuntu 安装docker

> $ sudo apt-get install  docker-engine

`没有可用软件包 docker-engine`

> $ sudo apt-get install  docker

## centOs 安装 
> $ sudo yum install docker

## 卸载

### Ubuntu彻底卸载Docker

- 卸载Docker CE
> $ sudo apt-get purge docker-ce

- 卸载Docker EE
> $ sudo apt-get purge docker-ee

-  删除Docker镜像、容器、数据卷等文件
> $ sudo rm -rf /var/lib/docker

 
 
