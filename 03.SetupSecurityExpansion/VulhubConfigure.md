## Vulhub环境配置过程

### 在虚拟机中安装ubuntu

### 安装vmware tools

进入系统，点击虚拟机-->安装tools，等待系统弹出tools的压缩包，将压缩包中的文件夹提取到桌面上，进入文件夹运行.pl文件，安装tools，第一个询问输入yes，之后一直回车就好了

### 换源

```
在Ubuntu系统上使用"apt-get install"进行软件安装更新的时候，由于使用的源是国外的，网络速度非常缓慢，本文记录在Ubuntu系统上进行更换国内源。
```

-  首先需要将原始的源文件进行备份，命令行如下：

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

- 接下来，修改源文件/etc/apt/sources.list，添加国内源：

```
sudo vim /etc/apt/sources.list
```

如果系统提示没有vim命令，可以 将vim改为vi或者先使用```sudo apt install vim-gnome```先安装vim

- 先将原文件的内容进行删除，然后添加国内源，常用的国内源有如下：

  - 阿里源

  ```
  deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
  deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
  ```

  - 清华源

  ```
  deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
  deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
  deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
  deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
  deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
  deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
  deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
  deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
  deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
  deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
  ```

  - 中科大源

  ```
  deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
  deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
  deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
  deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
  deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
  deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
  deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
  deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
  deb https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
  deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
  ```

  

  将上面给出的源复制到文件/etc/apt/sources.list即可。

- 最后，使用下面命令进行源更新：

  ```
  sudo apt-get update
  ```

### docker安装

注意：这里的命令的**运行顺序不能变**，

- 安装vim、curl

```
sudo apt install vim
```

```
sudo apt install curl
```

- 安装pip

```
curl -s https://bootstrap.pypa.io/get-pip.py | python3
```

- 安装docker

```
curl -s https://get.docker.com/ | sh
```

### 更换docker源

更换docker源需要修改docker/daemon.json文件，有的环境在安装了docker之后etc文件夹下面有可能没有docker文件夹，这个时候就需要自己创建文件。

文件创建好之后，修改daemon.json文件，添加源：

```
sudo vim daemon.json
```

源：

```
{
 "registry-mirrors": [
  "https://hub-mirror.c.163.com",
  "https://ustc-edu-cn.mirror.aliyuncs.com",
  "https://ghcr.io",
  "https://mirror.baidubce.com"
 ]
}
```

重启docker

```
service docker restart
```

### 安装docker-composer

```
sudo pip install docker-compose 
```

### 获取vulhub

- 安装git

```
sudo apt install git
```
- 克隆vulhub库

```
git clone https://github.com/vulhub/vulhub.git
```

### 漏洞复现

- 进入一个漏洞/环境目录

```
cd vulhub/httpd/CVE-2017-15715
```

- 自动化编译环境

```
sudo docker-compose build
```

- 启动整个环境

```
sudo docker-compose up -d
sudo docker-compose config	//查看运行的端口
```

- 查看本地ip地址

```
ifconfig
```

（ens33中的inet addr属性的值）

![网站复现1](imgs\网站复现1.png)

- 在浏览器中访问

![网站复现2](imgs\网站复现2.png)

- 删除整个环境

```
sudo docker-compose down -v
```

### 总结

```
vulhub靶场，可以复现各种各样的中间件的漏
```



### 参考博客

```
https://www.cnblogs.com/jerrylocker/p/10818650.html
https://www.cnblogs.com/jerrylocker/p/10818650.html
https://cloud.tencent.com/developer/article/1769231
```

