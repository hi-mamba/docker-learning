## []()

# docker-compose 命令说明


执行 docker-compose [COMMAND] --help 或者 docker-compose help [COMMAND] 可以查看具体某个命令的使用格式。

docker-compose 命令的基本的使用格式是
```shell script
docker-compose [-f=<arg>...] [options] [COMMAND] [ARGS...]
```
命令选项

-f, --file FILE 指定使用的 Compose 模板文件，默认为` docker-compose.yml`，可以多次指定。

-p, --project-name NAME 指定项目名称，默认将使用所在目录名称作为项目名。

--x-networking 使用 Docker 的可拔插网络后端特性

--x-network-driver DRIVER 指定网络后端的驱动，默认为 bridge

--verbose 输出更多调试信息。

-v, --version 打印版本并退出。



--compatibility 是兼容性命令 

up 是从拉取到构建到运行的全套指令

-d 是后台运行

