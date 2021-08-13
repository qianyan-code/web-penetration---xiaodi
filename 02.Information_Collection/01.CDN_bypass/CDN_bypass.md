## 信息收集-CDN绕过

```
简介：
	CDN的全称是Content Delivery Network，即内容分发网络。CDN是构建在现有网络基础之上的智能虚拟网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、内容分发、调度等功能模块，使用户就近获取所需内容，降低网络阻塞，提高用户访问响应速度和命中率。但在安全测试过程中，若目标存在CDN服务，将会影响到后续的安全测试过程。
	
如果目标有CDN服务，你直接对这个目标进行渗透的时候，渗透的是这个目标的缓存，不是真正意义上的目标
```



### 本节内容

- 如何判断目标存在CDN服务

  利用多节点技术进行请求返回判断

  ```
  在http://ping.chinaz.com/中输入网址进行ping检测，如果响应IP都相同则不存在CDN服务，存在不相同的则存在CDN服务。 
  ```

- CDN对于安全测试有哪些影响

- 目前常见的CDN绕过技术有哪些

  子域名查询

  ```
  例如news.xiaodi8.com是xiaodi8.com的子域名
  
  如果子域名和目标域名在同一服务器或者同一网段下对于CDN绕过的意义：
  	主站的流量一般比分站要多，有的管理员为了节省成本，只对主站做CDN服务，并不会对分站或子域名的站点做CDN服务，如果说子域名没有做CDN服务，则他的真实IP可以推算出主站IP
  ```

  邮件服务查询

  ```
  邮箱服务器一般不会做CDN
  ```

  国外地址请求

  ```
  有些网址是面向国内服务的，只设置了国内CDN，并没有设置国外的CDN，所以可以直接用国外地址来进行请求，这样有可能请求到的就是目标服务器的IP地址
  ```

  遗留文件，扫描全网

  黑暗引擎搜索特定文件

  ```
  https://www.shodan.io/
  https://www.zoomeye.org/
  https://fofa.so/
  ```

  dns历史记录，以量打量

  ```
  找它以前没有使用CDN时指向的地址
  
  以量打量：Dos攻击，耗尽网站的CDN服务的流量，不推荐使用，违法
  ```

  

- CDN真实IP地址获取后绑定指向地址

  更改本地HOSTS解析指向文件



### 本节演示案例

- 利用子域名请求获取真实IP

- 利用国外地址请求获取真实IP

- 利用第三方接口查询获取真实IP

- 利用邮件服务器接口获取真实IP

- 利用黑暗引擎搜索特定文件获取真实IP



- xueersi 	子域名上面的小技巧

  ![域名CDN设置](imgs\域名CDN设置.png)

- sp910 		DNS记录=第三方接口（接口查询）
    	https://get-site-ip.com/
    	https://x.threatbook.cn/（需要花钱，查询历史IP）
    	

- m.sp910（手机端网址）		子域名小技巧/采集/国外请求（同类型访问）

- mozhe		邮件源码测试对比第三方查询（地区分析）

    - 通过墨者邮箱绑定，发送邮件，通过邮件，查询IP地址

      ![墨者邮箱](imgs\墨者邮箱.png)

    - 通过发送的邮件查IP

      ![通过邮件查IP](imgs\通过邮件查IP.png)

      ![邮件原文](C:\Users\26554\Desktop\xiaodi-master\02.Information_Collection\02.CDN_bypass\imgs\邮件原文.png)

    - 通过邮件查询得到的IP地址为：219.153.49.169（百度之后显示的是重庆的IP）

    - 通过第三方查询（get-site-ip）得到的IP地址为：139.170.156.155（百度之后显示的是青海西宁的IP）

    - 得到的结果不同，这是该如何确定呢？两种方法，人情的（通过网站内容观察）和技术的

    - 人情的

      通过网站备案号，渝，表示这个公司是重庆的

      ![墨者网站详情1](imgs\墨者网站详情1.png)

      第三方找到的地址是青海的，所以根据这些分析，大概确定这个网站是重庆的

    - 技术的

      得到的IP地址为219.153.49.169
      
      修改本地hosts文件（在windows/system32/drives/etc下）
      
      ```
      219.153.49.111 mozhe.cn
      219.153.49.111 www.mozhe.cn
      ```
      
      在cmd中ping mozhe.cn或www.mozhe.cn看hosts文件是否修改成功
      
      修改成功之后访问mezhe.cn或者www.mozhe.cn，此时是不能访问的
      
      再修改本地hosts文件，将ip地址修改为得到的ip地址
      
      ```
      219.153.49.169 mozhe.cn
      219.153.49.169 www.mozhe.cn
      ```
      
      ping mozhe.cn观察hosts文件是否修改成功
      
      再刷新之前访问的网站，此时可以看到网站能够正常的打开，说明之前找到的IP地址就是这个网站的真实ip地址，并不是cdn的地址
      
      
      

- v23gg		黑暗引擎（shodan搜索指定hash文件）

    使用shodan中的icon文件的hash值来进行信息收集

    - 找到网站图标的地址

      网站图标

      ![网站图标](C:\Users\xiaodie\Desktop\xiaodi-master\02.Information_Collection\02.CDN_bypass\imgs\网站图标.png)

      关于网站图标的介绍：https://zhangge.net/4344.html

      获取网站图标

      1. 直接使用默认路径，目标网站/favicon.ico

         ……

    - 使用程序生成hash值

      ```python
      import mmh3
      import requests
      
      response = requests.get('https://www.bilibili.com/favicon.ico')
      favicon = response.content.encode('base64')
      hash = mmh3.hash(favicon)
      print('http.favicon.hash:'+str(hash))
      ```

      因为我安装了py2和py3，代码是在py2环境下的，安装库的时候直接使用pip安装的话是默认安装到py3中，所以需要使用```python2 -m pip install```给py2环境安装库，py2中的python.exe文件名我改成了python2，所以命令是python2，安装mmh3需要MS studio c++14.0的环境，所以需要先配好环境在安装，安装好MS之后，安装mmh3还是报错，，，（说是没有9.0的），之后通过网上的教程配置了一个环境变量，解决了这个问题，两个库安装完之后运行代码，就可以得到图标的hash值，复制输出到shodan中进行搜索

      ![环境变量](C:\Users\xiaodie\Desktop\xiaodi-master\02.Information_Collection\02.CDN_bypass\imgs\环境变量.png)

    - 使用shodan进行搜索

      ![搜索到的结果](C:\Users\xiaodie\Desktop\xiaodi-master\02.Information_Collection\02.CDN_bypass\imgs\搜索到的结果.png)

- 通过扫描全网绕过CDN获取网站IP地址

    - w8Fuckcdn（不建议使用）

    - fuckcdn

        ![how_to_use](C:\Users\xiaodie\Desktop\fuckcdn-master\fuckcdn-master\how_to_use.gif)

### 网站链接

https://www.shodan.io
https://x.threatbook.cn
http://ping.chinaz.com
https://www.get-site-ip.com/
https://asm.ca.com/en/ping.php
https://github.com/Tai7sy/fuckcdn
https://github.com/boy-hack/w8fuckcdn
https://mp.weixin.qq.com/s?__biz=MzA5MzQ3MDE1NQ==&mid=2653939118&idx=1&sn=945b81344d9c89431a8c413ff633fc3a&chksm=8b86290abcf1a01cdc00711339884602b5bb474111d3aff2d465182702715087e22c852c158f&token=268417143&lang=zh_CN#rd





  