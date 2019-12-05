

# docker-compose实践


## 编写docker-compose.yml文件

```yaml
version: '3'
services:
      web1:
         # 构建当前项目
         build: .
         # 镜像名称
         image: web1
         # 端口和暴露出来端口
         ports:
             - "9500:9005"
         volumes: 
             - /home/code/webtest:/code
         privileged: true
         restart: always
```
