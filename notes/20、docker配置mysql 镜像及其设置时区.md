
 


# docker配置mysql 镜像及其设置时区


## [docker mysql 镜像配置 bitnami/mysql](https://hub.docker.com/r/bitnami/mysql/)



## [Configure time zone to mysql docker container](https://stackoverflow.com/questions/49959601/configure-time-zone-to-mysql-docker-container)


- 这个配置在项目的 docker-compose.yaml 文件里面

```yaml

mysqldb:
    #image: mysql:5.7.21
    build: .
    #container_name: mysql_container
    ports:
      - "3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - TZ=Europe/Sofia
```

> 然后 连接docker 的mysql 镜像查看时区是否已经修改，
默认是UTC
