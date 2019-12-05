## [原文](https://blog.csdn.net/jiangyu1013/article/details/84572582)

# Docker 方式 部署 vue 项目 （docker + vue + nginx）


## 1.安装好 nginx 。

##2. 把 vue 项目的源码克隆到确定目录下。用 git 管理，所以直接 git clone 到既定目录就行了。

 如我的目录是：/root/jiangyu/projects/gentle_vue/gentle_vue_code 。

## 3. 项目打包：

 npm run build 
会自动生成 dist 文件夹 。

## 4. 在任意目录下新建文件  dockerfile 。内容如下：
```dockerfile
# 设置基础镜像
FROM nginx
# 定义作者
MAINTAINER jiangyu
# 将dist文件中的内容复制到 /usr/share/nginx/html/ 这个目录下面
COPY dist/  /usr/share/nginx/html/
```
## 5. 构建镜像：   
```
# -t 是给镜像取名。
# 最后有一个点 “.”，表示使用当前路径下的 dockerfile 文件，也可以指定使用其它路径的。
docker build -t gentle-vue . 
```
查看新生成的镜像：
```docker
docker images
```

## 6.启动容器：
```
# -p ：配置端口映射，格式是外部访问端口：容器内端口
# -d ：后台运行  
# --name : 给容器取名
# 最后有 2 个 gentle-vue,前面一个是给容器取的名字，后面一个是使用的镜像的名字
```

```docker
 docker run -p 3000:80 -d --name gentle-vue gentle-vue
```

查看是否运行成功：



## 7. 浏览器访问
 