# Burpsuite抓包修改测试

### 使用burpsuite模拟目录扫描工具的原理

实验环境：Firefox+Burpsuite（可抓取https）

**配置浏览器的代理IP和端口，将burpsuite抓包的IP和端口设置成和浏览器相同的**，接下来开始实验

以xiaodi8.com为例

首先抓取xiaodi8.com的数据包

![case11](imgs\case11.png)

![case12](imgs\case12.png)

![case13](imgs\case13.png)

![case14](imgs\case14.png)

![case15](imgs\case15.png)

总结：以上通过更改请求数据包的请求头中的请求资源路径，得到了200、301、404三种不同的状态码，目录扫描工具的原理也和这个类似