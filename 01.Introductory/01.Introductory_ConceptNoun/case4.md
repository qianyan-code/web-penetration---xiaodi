# APP类结合WEB协议，PC类结合WEB协议

### APP类结合WEB协议

实验环境：Firefox+Burpsuite（可抓取https）、逍遥模拟器

目标：将在模拟器中找到的内容，在电脑网页上进行显示（以一篇文章为例）

思路：

- 修改模拟器传输数据包的路径

  ![case41](imgs\case41.png)

  ![case42](imgs\case42.png)

- 使用Burpsuite抓取配置的路径上传输的数据包

  ![case43](imgs\case43.png)

  ![case44](imgs\case44.png)

  打开模拟器，选择要抓包的软件，从里面随便选择一篇文章

  ![case45](imgs\case45.png)

  清空HTTP history

  ![case46](imgs\case46.png)

  ![case47](imgs\case47.png)

  ![case48](imgs\case48.png)

- 更改浏览器的传输数据包的路径，使Burpsuite抓取浏览器传输的数据包

  打开浏览器-->工具-->选项-->高级-->网络-->连接-->设置

  ![case49](imgs\case49.png)

  ![case410](imgs\case410.png)

- 根据抓取到的模拟器中的数据包中的host找到要访问的网站的地址

  ![case411](imgs\case411.png)

  ![case412](imgs\case412.png)



**因为太菜了，后面两部暂时没有完成，如果会了再回来改**

- 在浏览器中输入，无法打开，因为使用pc端产生的数据包和用手机产生的数据包是不相同的
- 用Burpsuite抓取浏览器发送的数据包，将数据包的内容改为之前抓到的模拟器产生的数据包
- 如果访问成功，则说明实验成功

总结：第一节的演示案例，原理不太懂，结果也只做出了一点，小迪老师应该就是想要让我们知道app上的内容，可以通过抓包找到对应的网页上的内容



### PC类结合WEB协议

使用WSExplorer进行进程抓包（需要以管理员身份运行）

抓到的结果

![case413](imgs\case413.png)

完全看不懂什么意思。。。。