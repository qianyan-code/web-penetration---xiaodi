## Vulhub环境配置过程

### 在虚拟机中安装ubuntu

### 安装vmware tools

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

  