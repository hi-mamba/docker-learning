## [原文](https://blog.csdn.net/SoberChina/article/details/84849860)

# docker容器 java 默认读取系统时区问题

## 基于alpine构建的java基础镜像时区问题

### alpine简介

alpine 是一个面向安全的轻型的Linux发行版。大小只有几兆。

我们基于alpine基础镜像构建我们的docker image dockerfile配置如下:
```dockerfile
FROM openjdk:8-jdk-alpine
COPY /target/app-0.0.1-SNAPSHOT.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
## 问题
启动服务查看日志，发现日志比现在的时间少8个小时，java时区默认读取的系统时区，随手执行了一下date -R
```shell script
$ date -R
Wed, 05 Dec 2018 10:16:15 +0800
```
系统时区是东八区，java时区默认读取系统时区 时间不应该少8个小时，然后具体有分析了一遍TimeZone类
```java
/**
* 获取默认时区
*/
public static TimeZone getDefault() {
        return (TimeZone) getDefaultRef().clone();
    }

    /**
  * Returns the reference to the default TimeZone object. This
  * method doesn't create a clone.
  */
 static TimeZone getDefaultRef() {
     TimeZone defaultZone = defaultTimeZone;
     if (defaultZone == null) {
         // Need to initialize the default time zone.
         defaultZone = setDefaultZone();
         assert defaultZone != null;
     }
     // Don't clone here.
     return defaultZone;
 }

 private static synchronized TimeZone setDefaultZone() {
     TimeZone tz;
     // get the time zone ID from the system properties
     String zoneID = AccessController.doPrivileged(
             new GetPropertyAction("user.timezone"));

     // if the time zone ID is not set (yet), perform the
     // platform to Java time zone ID mapping.
     if (zoneID == null || zoneID.isEmpty()) {
         String javaHome = AccessController.doPrivileged(
                 new GetPropertyAction("java.home"));
         try {
            //重点这句话
             zoneID = getSystemTimeZoneID(javaHome);
             if (zoneID == null) {
                 zoneID = GMT_ID;
             }
         } catch (NullPointerException e) {
             zoneID = GMT_ID;
         }
     }
      //注意这句话
     // Get the time zone for zoneID. But not fall back to
     // "GMT" here.
     tz = getTimeZone(zoneID, false);

     if (tz == null) {
         // If the given zone ID is unknown in Java, try to
         // get the GMT-offset-based time zone ID,
         // a.k.a. custom time zone ID (e.g., "GMT-08:00").
         String gmtOffsetID = getSystemGMTOffsetID();
         if (gmtOffsetID != null) {
             zoneID = gmtOffsetID;
         }
         tz = getTimeZone(zoneID, true);
     }
     assert tz != null;

     final String id = zoneID;
     AccessController.doPrivileged(new PrivilegedAction<Void>() {
         @Override
             public Void run() {
                 System.setProperty("user.timezone", id);
                 return null;
             }
         });

     defaultTimeZone = tz;
     return tz;
 }

 /**
  * Gets the platform defined TimeZone ID.
  **/
 private static native String getSystemTimeZoneID(String javaHome);
```
最终发现getSystemTimeZoneID(String javaHome)方法为本地方法。
当然具体深究的话需要看JDK源码(openJDK上有完整的JDK源代码)。随手百度是个好习惯，这篇文章写得不错;
[Java读取系统默认时区](https://www.cnblogs.com/darange/p/9368245.html)

## 在Linux系统上，大概过程为以下几步：
```
先找TZ变量，没有，到2。
读/etc/timezone，没有到3。
比较/etc/localtime文件与"/usr/share/zoneinfo目录下所有时区文件，如果有一致的，就为该时区，如果没有，到4,
默认为标准GMT。
```
大致知道了这个过程，然后开始分析docker container ,进入容器查看相应的目录结构，echo $TZ 无输出 到2，
未找到timezone文件 转3 有localtime 文件(再启动容器的时候localtime是挂载进去的) 
然后再去查看ls /usr/share/zoneinfo 未找到该目录，最终发现alpine基础镜像并没有时区文件。

## ok 问题最终找到，解决此类问题几种解决方法:

- 第一种: 挂载时区文件；

- 第二种: 配置TZ环境变量；

- 第三种: Dockerfile 添加RUN echo "Asia/Shanghai" > /etc/timezone 配置
 