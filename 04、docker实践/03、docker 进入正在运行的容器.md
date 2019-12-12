

# docker 进入正在运行的容器

## 用法：
> docker exec [OPTIONS] CONTAINER COMMAND [ARG…]

如一个正在运行的容器ID为 9527abc，进入容器里的命令如下:

> docker exec -it 9527abc /bin/bash

