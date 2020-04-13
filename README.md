# java_security

### JAVA安全实现三种方式：
    1.JDK 2.Commons Codec 3.Bouncy Castle

====
#### 一。非对称加密算法：com.timliu.security.asymmetric_encryption
    1.DH 2.RSA 3.ElGamal

####  二。Base64：com.timliu.security.base64
    1.JDK实现 2.common codes实现 3.bouncy castle实现

####  三。消息摘要算法：com.timliu.security.message_digest
    1.MD5 2.SHA 3.MAC

####  四。数字签名:JDK实现  com.timliu.security.signature
    1.RSA 2.DSA 3.ECDSA

####  五。对称加密算法：com.timliu.security.symmetric_encryption
    1.3DES 2.AES 3.PBE
    
 
    
====
####   非对称加密算法中“ElGamal” ，的异常问题：
    对于：“Illegal key size or default parameters”异常，是因为美国的出口限制，Sun通过权限文件（local_policy.jar、US_export_policy.jar）做了相应限制。因此存在一些问题.
Java 6 无政策限制文件：[java官方下载](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html) 本 jce_policy-6.zip 包已经下载到本项目的ext目录下。

Java 7 无政策限制文件：[java官方下载](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) 本 UnlimitedJCEPolicyJDK7.zip 包已经下载到本项目的ext目录下。
    
    我的macbook 10.10.2安装的是java7：
    到：/Library/Java/JavaVirtualMachines/jdk1.7.0_71.jdk/Contents/Home/jre/lib/security 目录下，对应覆盖local_policy.jar和US_export_policy.jar两个文件。
    
    windows的系统可能需要如下操作：
    切换到%JDK_Home%\jre\lib\security目录下，对应覆盖local_policy.jar和US_export_policy.jar两个文件。同时，你可能有必要在%JRE_Home%\lib\security目录下，也需要对应覆盖这两个文件。
 
#### jBCrypt

[jBCrypt网站](https://www.mindrot.org/projects/jBCrypt/)

[已下载源码](https://github.com/itning/java_security/blob/master/libs/jBCrypt-0.4.zip)

RSA私钥A加密请求
私钥A如何获取？

RSA签名
RSA加密


服务器使用私钥B发送加密后的用于签名的随机私钥A（随机公钥A在服务器存储）
JS用公钥B解密获取私钥A（私钥A随后存储在sessionStorage）。
使用私钥A签名数据发送给服务器
服务器使用公钥A验证数据正确性

公钥B怎么来？
放在前端，每隔一段时间更换

服务器存储：
用于验签的随机公钥A---存储在用户表中
用于加密的私钥B----存储在配置文件中
前端存储：
用于签名的私钥A----存储在sessionStorage
用于解密的公钥B----硬编码，隔一段时间更换

数据中包含时间戳 10秒后过期。
