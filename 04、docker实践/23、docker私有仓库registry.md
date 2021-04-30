##### [参考](https://www.sudo.ren/article/17)


# docker私有仓库registry


假如你有一个私有的仓库 
> reg.mamba.com


在本地打镜像

> docker build -t reg.mamba.com/kobe/docker-maven-mysql:1.0.0 .

登录这个仓库
> docker login reg.mamba.com

> 用户名

> 密码

上传到私有仓库

> docker push reg.mamba.com/kobe/docker-maven-mysql:1.0.0
