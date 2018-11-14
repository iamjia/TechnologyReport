# iOS 应用防 HTTPS MiTM 基本方案


## HTTPS MiTM

* [三种解密 HTTPS 流量的方法介绍](https://imququ.com/post/how-to-decrypt-https.html)


## 防 MiTM 原理

* [HTTP Public Key Pinning 介绍](https://imququ.com/post/http-public-key-pinning.html)


## 实现方案 SSL pinning

### 面临的问题

1、叶子证书问题


2、证书过期问题

3、越狱后替换证书绕过


### 代码实现

1、[Swift 方案参考](https://medium.com/@kennethpoon/lets-write-swift-code-to-intercept-ssl-pinning-https-requests-12446303cc9d)


2、Objective-C + AFNetworking 方案