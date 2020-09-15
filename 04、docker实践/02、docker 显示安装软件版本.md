

# docker 显示安装软件版本

```shell script
[root@localhost docker-java]# docker images
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
openjdk                           8                   09df0563bdfc        10 days ago         488MB
python                            latest              0a3a95c81a2b        10 days ago         932MB
mamba/puppeteer-docker-example   latest              7354071777c1        11 days ago         1.2GB
mysql/mysql-server                latest              b172b40598f0        7 weeks ago         350MB
openjdk                           8-jdk-alpine        a3562aa0b991        6 months ago        105MB
hello-world                       latest              fce289e99eb9        11 months ago       1.84kB
[root@localhost docker-java]# docker run -it --rm openjdk:8 bash
root@a51edd412d60:/# java -version
openjdk version "1.8.0_232"
OpenJDK Runtime Environment (build 1.8.0_232-b09)
OpenJDK 64-Bit Server VM (build 25.232-b09, mixed mode)
root@a51edd412d60:/# exit
exit

```


```shell script
[root@localhost docker-java]# docker run -it --rm python:latest bash
root@1e645b65683b:/# ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
root@1e645b65683b:/# pwd
/
root@1e645b65683b:/# python -V
Python 3.8.0
```