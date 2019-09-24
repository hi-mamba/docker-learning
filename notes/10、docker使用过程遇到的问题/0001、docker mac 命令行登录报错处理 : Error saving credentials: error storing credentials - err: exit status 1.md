## [原文](https://blog.csdn.net/xufwind/article/details/88756557)

# docker mac 命令行登录报错处理 : Error saving credentials: error storing credentials - err: exit status 1

比较新版本的docker命令行登录会出现以下错误:

> Error saving credentials: error storing credentials - err: exit status 1, out: `The user name or passphrase you entered is not correct.`
>
在网上找了很久，总算找个一个能用的:以下为具体操作

1. 点开启动台，搜索 Keychain Access并点开, 或是点开 访达(findder) -> 应用程序(applications) -> 实用工具(utilities) ->钥匙串访问(Keychain Access)

2. 右键点击登录 -> 锁定钥匙串登录，再解锁钥匙串登录就可以了，注意解锁的时候需要输入mac登录密码
 
原文链接：<https://blog.csdn.net/xufwind/article/details/88756557>