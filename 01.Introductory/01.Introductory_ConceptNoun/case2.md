# DNS解析修改后分析（本地或服务）

hosts一般在C:\Windows\System32\drivers\etc中

当我们ping一个IP地址时，计算机会首先检查hosts文件中有没有对应的域名解析，没有的话再到DNS中去寻找
例子:

没有加之前直接 ping xiaodi8.com

![case21](imgs\case21.png)

如果在hosts文件中加一行 1.2.3.4 xiaodi8.com，ping xiaodi8.com时，会自动解析为1.2.3.4

![case22](imgs\case22.png)



### 总结

如果我们能够修改对方的hosts文件，则可以修改对方要访问的网站指向的域名，例如网上的钓鱼网站。

steam游戏加速下载也有可能会用到



