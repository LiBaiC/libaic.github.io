---
title: 多git账户情况下Hexo博客部署
date: 2017-03-02 16:21:42
---
# 问题
最近在使用Hexo搭建博客时碰到很多问题，其中之一便是如果之前PC终端已使用git搭建过博客，现在需要在同一台终端上使用不同的git账户再搭建博客，就会在部署时
 ![hexod](https://cl.ly/382R3o3v0U3g/1.png)
提示
ERROR: Permission to A/A.github.com.git denied to B.
导致失败。
***
# 解决办法
* ##### 1 首先取消git全局设置，输入这两条命令
 ![unset](https://cl.ly/16293L0h0Q3f/2.png)
	
* ##### 2 添加新的Shh配置
  ![pic4](https://cl.ly/1N330B1W1W0o/3.png)
之后会提示你输入文件名，区别第一个默认名称“id_rsa”就可以,假设为“id_rsa_B”。把新生成的公钥加入到你第二个git账号。

* ##### 3 如果c:\Users\yourname\.ssh 目录下没有config文件，新建一个
  ![pic4](https://cl.ly/0n2g1T1H3g3O/4.png)
  打开config文件，进行配置
  ![pic4](https://cl.ly/1m0Q3m3Y3U2G/5.png)

* ##### 4 进入你部署博客根目录，打开_config.yml文件，修改Repository，变为
  ![pic4](https://cl.ly/2D1s1G3a1o2K/6.png)

* #####5 进入git bash按原流程重新提交部署，你会发现需要第二个秘钥"id_rsa_B"的密码
  ![hexod](https://cl.ly/382R3o3v0U3g/1.png)
  

# 原因
我们可以发现 ssh 客户端是通过类似: git@github.com:A/A.github.com.git 这样的 git 地址中的 User 和 Host 来识别使用哪个本地私钥的。 很明显，如果 User 和 Host 始终为 git 和 github.com，那么就只能使用一个私钥。 所以需要上面的方式配置，每个账号使用了自己的 Host，每个 Host 的域名做 CNAME 解析到 github.com，这样 ssh 在连接时就可以区别不同的账号了。