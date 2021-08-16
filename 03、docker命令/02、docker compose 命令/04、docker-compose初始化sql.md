[Docker Compose MySql initdb](https://onexlab-io.medium.com/docker-compose-mysql-initdb-4c3388047dea)

#  docker-compose初始化sql

> MYSQL_SERVICE_USER: 用户名  #注意这里不能初始化用户名为 user,我初始化为user 日志有error

![image](https://user-images.githubusercontent.com/7867225/129573928-b0248ac2-d0ec-46bc-882e-54fa4a116b6c.png)

![image](https://user-images.githubusercontent.com/7867225/129574204-f8efec99-6ca4-470d-872d-ffb6bcc7a4d0.png)


我的配置文件

```yaml
version: '3'

services:
  mysql5.7:
    image: mysql:5.7
    container_name: mysql57
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: mamba
      MYSQL_DATABASE: nacos
      MYSQL_USER: mamba
      MYSQL_PASSWORD: mamba
    ports:
      - 3306:3306
    volumes:
      - ./docker/mysql:/docker-entrypoint-initdb.d
  nacos:
    image: nacos/nacos-server:2.0.3
    container_name: nacos
    restart: always
    depends_on:
      - mysql5.7
    environment:
      PREFER_HOST_MODE: hostname #如果支持主机名可以使用hostname,否则使用ip，默认也是ip
      SPRING_DATASOURCE_PLATFORM: mysql #数据源平台 仅支持mysql或不保存empty
      MODE: standalone
      MYSQL_SERVICE_HOST: mysql5.7
      MYSQL_SERVICE_DB_NAME: nacos
      MYSQL_SERVICE_PORT: 3306
      MYSQL_SERVICE_USER: mamba  # 注意这里不能初始化用户名为 user
      MYSQL_SERVICE_PASSWORD: mamba
      NACOS_APPLICATION_PORT: 8848
      JVM_XMS: 512m
      JVM_MMS: 320m
    #volumes:
    #  - ./docker/nacos/standalone-logs/:/home/nacos/logs
    #  - ./docker/nacos/plugins/:/home/nacos/plugins
    #  - ./docker/nacos/conf/application.properties:/home/nacos/conf/application.properties
    ports:
      - "8848:8848"
```

nacos 数据库地址

https://github.com/alibaba/nacos/blob/develop/distribution/conf/nacos-mysql.sql


注意：我修改下数据库文件，添加使用数据库

> use nacos;
