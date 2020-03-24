
##### [原文1](https://blog.csdn.net/huangjinao/article/details/101078391)

##### [原文2](https://www.cnblogs.com/heyangyi/p/9288402.html)

#  docker安装多个mysql并启动

### 创建目录
> 如果需要挂载，否则就不需要创建了

```shell script
mkdir /data/mysql/data5.7

mkdir /data/mysql/data8.0
```
### 添加镜像
```shell script
docker pull mysql:5.7
docker pull mysql/mysql-server
```
### 启动镜像（一个跑在默认的3306上、另一个跑在3307上）

5.7 启动
```shell script
docker run --name mysql_old -e MYSQL_ROOT_PASSWORD=123456 -d -p 3316:3316 mysql:5.7
```
> mysql -uroot -p -P 3316
>> 密码好像不需要可以登录

8.0 启动
```shell script
docker run --name mysql_8_image -e MYSQL_ROOT_PASSWORD=123456 -d -p 3307:3307 mysql/mysql-server:latest
```
登录MYSQL,如果遇到  mysql.sock 问题的应该就是没有初始化好.
```shell script
bash-4.2# mysql -uroot -P 3307 -p
```

- mysql_8_image是容器名称，通过--name指令指定
- 123456为数据库root的密码，通过-e指定环境MYSQL_ROOT_PASSWORD为123456，-e （指定容器内的环境变量）
- -d 使用-d参数，容器会进入到后台，用户无法看到容器中的信息，也无法进行操作
- 3307:3306 为端口映射，指定本地主机端口3307映射到容器的3306端口