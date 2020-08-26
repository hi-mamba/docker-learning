# Error response from daemon: Unknown instruction

Docker daemon在执行Dockfile的指令前，会做检查，如果有`语法错误`会报错，

$ docker build -t test/myapp .

Sending build context to Docker daemon 2.048 kB
Error response from daemon: Unknown instruction: RUNCMD
