## [Docker Alpine 镜像设置东八区](https://blog.kelu.org/tech/2018/10/01/docker-alpine-timezone.html)

## [How can I set the timezone please](https://github.com/gliderlabs/docker-alpine/issues/136)

# Docker Alpine 镜像设置东八区

```dockerfile
FROM alpine:3.6
RUN apk update && apk add --no-cache tzdata
ENV TZ Asia/Shanghai
```

>  docker run -it --rm alpine /bin/sh