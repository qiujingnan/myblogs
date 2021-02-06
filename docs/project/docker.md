```
>  以下所有的命令都是基于 Windows 下 WSL 创建的 Ubuntu 18.04 ，如果你在尝试下面的命令中出错的话可以自行搜索解决 ，也欢迎留言讨论交流
```
今天学习一下创建自己的 docker

### 基础命令解释

直接在命令行中输入 **docker** 即可看到下列信息，目前我们只关注一些常用的命令即可


```bash
$ docker run     # 启动一个实例
$ docker stop    # 停止
$ docker restart # 重启
$ docker ps		 # 查看所有的实例
$ docker images  # 查看已经下载安装的 images
```

目前我们只需要了解这些命令即可，下面我们来尝试运行第一个例子吧



### 一个简单的例子
首先我们需要更换镜像源，否则下载速度会很慢
#### 国内加速服务

- 网易：https://hub-mirror.c.163.com/
- 阿里云：https://<你的 ID>.mirror.aliyuncs.com
- 七牛云加速器：https://reg-mirror.qiniu.com
当配置某一个加速器地址之后，若发现拉取不到镜像，请切换到另一个加速器地址。国内各大云服务商均提供了 Docker 镜像加速服务，建议根据运行 Docker 的云平台选择对应的镜像加速服务。

由于上一篇文章我们刚刚注册了阿里云账号，我们这里选择阿里云

登录我们上次注册的[阿里云官网](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors) ，在 镜像工具 > 镜像加速器 中复制他提供的网站

右击右下角 Docker 图标 > setting > Docker Engine ，将刚才的网址复制到 registry-mirrors 中

> 其他加速方式可以参考这个[网站](https://www.runoob.com/docker/docker-mirror-acceleration.html)

#### 运行 HelloWorld

我们创建一个新的 Ubuntu 虚拟机并让这个虚拟机运行一句话
```bash
$ docker run ubuntu:15.10 /bin/echo "Hello world"
```
这时在屏幕中就会输出 "Hello world"

我们进入 Ubuntu 虚拟机，并执行一些 Linux 命令
```bash
$ docker run -i -t ubuntu:15.10 /bin/bash
```

- -t：在新容器内指定一个伪终端或终端。

- -i： 允许你对容器内的标准输入 (STDIN) 进行交互

这时我们已经进入了新建的虚拟机中，可以执行一些 Linux 命令例如
```bash
root@3a3051447e22:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@3a3051447e22:/# cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=15.10
DISTRIB_CODENAME=wily
DISTRIB_DESCRIPTION="Ubuntu 15.10"
```

随后我们直接 ctrl + D 或者 输入 exit 即可退出虚拟机

#### 后台运行虚拟机
上述的方法在你退出之后后台不会留有进程，相当于你运行了一个程序，完成后即退出

在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 **-d **指定容器的运行模式。

```bash
$ docker run -itd --name ubuntu-test ubuntu /bin/bash
```

此时我们再想进入虚拟机有两种方式

```
$ docker exec -it 243c32535da7 /bin/bash
or
$ docker attach 1e560fca3906 
```

使用 attach 之后如果退出虚拟机，那么虚拟机也不会在后台继续运行

而使用 exec 之后虚拟机还是会继续在后台运行


### 其他的一些命令
#### 导入导出
```bash
$ docker export 1e560fca3906 > ubuntu.tar
$ cat docker/ubuntu.tar | docker import - test/ubuntu:v1
```
export 导出 
import 导入

#### 删除
```bash
$ docker rm -f dockerID
```