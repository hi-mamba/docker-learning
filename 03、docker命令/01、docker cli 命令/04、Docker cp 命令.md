
# [Docker cp 命令](https://www.runoob.com/docker/docker-cp-command.html)

docker cp :用于容器与主机之间的数据拷贝


## 实例

将主机/www/test 目录拷贝到容器96f7f14e99ab的/www目录下。

> docker cp /www/test 96f7f14e99ab:/www/

将主机 test.jar 拷贝到容器96f7f14e99ab的/www目录下。

> docker cp test.jar 96f7f14e99ab:/www/
