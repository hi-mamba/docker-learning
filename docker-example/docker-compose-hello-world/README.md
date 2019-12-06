

# WHY

## 为什么使用docker-compose?
如果采用docker run的方式一个一个容器去创建十分麻烦。
为了能更高效的批量创建容器，docker推出了docker-compose工具.

compose把构建镜像，运行容器两个步骤放在一个yml文件里配置，实现自动化部署。

有了docker-compose 我们就不需要安装Java，python环境了，只需要在镜像那里指定就可以了,
而且不需要到处配置环境


## WHAT
在这个项目 docker-compose-hello-world 当前目录执行下面命令
```shell script
$ docker-compose -f docker-compose-hello-world.yml up
```

## 查看日志

```shell script
$ docker-compose -f docker-compose-hello-world.yml logs
```

如果修改了文件，需要 build

```shell script
$ docker-compose -f docker-compose-hello-world.yml down

$ docker-compose -f docker-compose-hello-world.yml up --build
```