
# docker run 和 docker-compose 配置挂载 Volume


  volumes:
  - ./app:/mnt/app

这样本地的当前目录下的 app 这个目录里的东西，跟容器里的 /mnt/app 这个目录就是同步的了

> 冒号左边是服务器保存logs文件的路径(可以自己定义),右边是docker 容器的路径

