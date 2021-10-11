<https://www.cnblogs.com/mydailycoding/p/12375352.html>

# WSL 出现:Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running

解决方案：

> $ sudo /etc/init.d/docker start

启动docker之后便不再出现片头那个问题

