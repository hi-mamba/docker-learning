## [Run a Java application in a Docker container](https://www.jetbrains.com/help/idea/running-a-java-app-in-a-container.html)

# 04、IDEA 执行dockerfile文件

## Run the Java application in a container #
In the Project tool window, right-click the project name, point to New and click File.

In the New File dialog, type Dockerfile and click OK.

Type the following in the new Dockerfile:
```dockerfile
FROM openjdk:8
# 注意这个文件，在docker 设置好的 file sharing 里面设置的文件夹
COPY ./out/production/DockerJavaApp/ /tmp
WORKDIR /tmp
ENTRYPOINT ["java","Main"]
Click the Run on Docker gutter icon (The Run button) and then click Run on 'Docker'.
```