## [原文](https://www.qikegu.com/docs/3033)

# Docker Java 例子

## 1. 创建项目目录
我们会把这个项目的相关文件，集中放到一个目录docker-java：
```shell script
[root@qikegu demo]# mkdir docker-java
```

## 2. 创建Java文件
在docker-java目录下，创建一个Java文件：
```java
public class Qikegu{
    public static void main(String[] args){
        System.out.println("This is java docker app - qikegu.com \n");
    }
}
```

## 3. 创建Dockerfile
创建Java文件之后，我们需要创建一个Dockerfile，其中包含了Docker的指令。
在docker-java目录下创建Dockerfile，文件名必须是Dockerfile。

Dockerfile
```dockerfile
FROM java:8
COPY . /var/www/java
WORKDIR /var/www/java
RUN javac Qikegu.java
CMD ["java", "Qikegu"]
```
所有指令都大写，这是惯例。

现在docker-java目录下有2个文件：
```shell script
[root@qikegu docker-java]# ls
Dockerfile  Qikegu.java
```

## 4. 构建 Docker 镜像
切换到docker-java目录，运行docker build -t qikegu-java . 命令，构建Docker镜像。
Docker镜像可以任意取名，此处命名为qikegu-java。
```shell script
[root@qikegu docker-java]# docker build -t qikegu-java .
Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM java:8
 ---> d23bdf5b1b1b
Step 2/5 : COPY . /var/www/java
 ---> Using cache
 ---> 7f24b5fc6fb6
Step 3/5 : WORKDIR /var/www/java
 ---> Using cache
 ---> 2eacd7222454
Step 4/5 : RUN javac Qikegu.java
 ---> Using cache
 ---> bf254a2eec11
Step 5/5 : CMD ["java", "Qikegu"]
 ---> Using cache
 ---> 1842ec92df2d
Successfully built 1842ec92df2d
Successfully tagged qikegu-java:latest
```
```shell script
[root@qikegu docker-java]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
qikegu-java         latest              1842ec92df2d        13 minutes ago      643MB
<none>              <none>              327ab0702d14        14 minutes ago      643MB
...
```
这里，最后使用docker images查看镜像，可以看到构建镜像成功。接下来就可以运行镜像了。

## 5. 运行 Docker 镜像
执行docker run qikegu-java命令运行镜像：
```shell script
[root@qikegu docker-java]# docker run qikegu-java
This is java docker app - qikegu.com
```
可以看到，qikegu-java镜像成功运行，输出了一条信息。


## ps 如果遇到不输出的

比如我的镜像是这个。。。。死活就是没有输出出来
```dockerfile
FROM openjdk:8-jdk-alpine
COPY . /var/www/java
WORKDIR /var/www/java
RUN javac TimeZoneExample.java
CMD ["java", "TimeZoneExample"]

FROM alpine:3.6
RUN apk update && apk add --no-cache tzdata
ENV TZ=Asia/Shanghai

RUN echo "Asia/Shanghai" > /etc/timezone
```

TimeZoneExample.java
```Java
import java.time.ZoneId;


public class TimeZoneExample {
    public static void main(String[] args) {
        System.out.println("ZoneId={}"+ZoneId.systemDefault().getId());
    }
}
```

需要调整下  dockerfile文件

```dockerfile

FROM alpine:3.6
RUN apk update && apk add --no-cache tzdata
ENV TZ=Asia/Shanghai

FROM openjdk:8-jdk-alpine
COPY . /var/www/java
WORKDIR /var/www/java
# 注意这里的顺序
RUN echo "Asia/Shanghai" > /etc/timezone
RUN javac TimeZoneExample.java
CMD ["java", "TimeZoneExample"]
```
如果还有MYSQL 之类的时区也记得设置