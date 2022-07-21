> 从 2017 年 3 月开始 docker 在原来的基础上分为两个分支版本: Docker CE 和 Docker EE：Docker CE 即社区免费版；Docker EE 即企业版，强调安全，但需付费使用；按照官网上 Docker Engine - Community 包现在就是叫做 Docker CE。

### Docker 架构

Docker 包含三个基本概念：

* **镜像**：Docker 镜像（Image），就相当于是一个 root 文件系统。

* **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。

* **仓库（Repository）**：仓库可看着一个代码控制中心，用来保存镜像。

#### 镜像（Image）

我们都知道，操作系统分为 **内核** 和 **用户空间**。对于 `Linux` 而言，内核启动后，会挂载 `root` 文件系统为其提供用户空间支持。而 **Docker 镜像**（`Image`），就相当于是一个 `root` 文件系统。比如官方镜像 `ubuntu:18.04` 就包含了完整的一套 Ubuntu 18.04 最小系统的 `root` 文件系统。

**Docker 镜像** 是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像 **不包含** 任何动态数据，其内容在构建之后也不会被改变。

因为镜像包含操作系统完整的 root 文件系统，其体积往往是庞大的，因此在 Docker 设计时，就充分利用`Union FS`的技术，将其设计为**分层存储**的架构。所以严格来说，镜像并非是像一个 ISO 那样的打包文件，镜像只是一个虚拟的概念，其实际体现并非由一个文件组成，而是由一组文件系统组成，或者说，由多层文件系统联合组成。

镜像构建时，会一层层构建，前一层是后一层的基础。每一层构建完就不会再发生改变，后一层上的任何改变只发生在自己这一层。比如，删除前一层文件的操作，实际不是真的删除前一层的文件，而是仅在当前层标记为该文件已删除。在最终容器运行的时候，虽然不会看到这个文件，但是实际上该文件会一直跟随镜 像。因此，在构建镜像的时候，需要额外小心，每一层尽量只包含该层需要添加的东西，任何额外的东西应该在该层构建结束前清理掉。

分层存储的特征还使得镜像的复用、定制变的更为容易。甚至可以用之前构建好的镜像作为基础层，然后进一步添加新的层，以定制自己所需的内容，构建新的镜像。

#### 容器（Container）

镜像（`Image`）和容器（`Container`）的关系，就像是面向对象程序设计中的 `类` 和 `实例` 一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。

容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的 命名空间。因此容器可以拥有自己的 root 文件系统、自己的网络配置、自己的进程空间，甚至自己的用户 ID 空间。容器内的进程是运行在一个隔离的环境里，使用起来，就好像是在一个独立于宿主的系统下操作一样。这种特性使得容器封装的应用比直接在宿主运行更加安全。也因为这种隔离的特性，很多人初学 Docker 时常常会混淆容器和虚拟机。

前面讲过镜像使用的是分层存储，容器也是如此。每一个容器运行时，是以镜像为基础层，在其上创建一个当前容器的存储层，我们可以称这个为容器运行时读写而准备的存储层为 **容器存储层**。

容器存储层的生存周期和容器一样，容器消亡时，容器存储层也随之消亡。因此，任何保存于容器存储层的信息都会随容器删除而丢失。

按照 Docker 最佳实践的要求，容器不应该向其存储层内写入任何数据，容器存储层要保持无状态化。所有的文件写入操作，都应该使用数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主（或网络存储）发生读写，其性能和稳定性更高。

数据卷的生存周期独立于容器，容器消亡，数据卷不会消亡。因此，使用数据卷后，容器删除或者重新运行之后，数据却不会丢失。

#### 仓库（Repository）

镜像构建完成后，可以很容易的在当前宿主机上运行，但是，如果需要在其它服务器上使用这个镜像，我们就需要一个集中的存储、分发镜像的服务，[Docker Registry](https://vuepress.mirror.docker-practice.com/repository/registry.html) 就是这样的服务。

一个 **Docker Registry** 中可以包含多个 **仓库**（`Repository`）；每个仓库可以包含多个 **标签**（`Tag`）；每个标签对应一个镜像。

通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本。我们可以通过 `<仓库名>:<标签>` 的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以 `latest` 作为默认标签。

以Ubuntu 镜像为例，ubuntu 是仓库的名字，其内包含有不同的版本标签，如，16.04, 18.04。我们可以通过 ubuntu:16.04，或者 ubuntu:18.04 来具体指定所需哪个版本的镜像。如果忽略了标签，比如 ubuntu，那将视为 ubuntu:latest。

仓库名经常以 *两段式路径* 形式出现，比如 `jwilder/nginx-proxy`，前者往往意味着 Docker Registry 多用户环境下的用户名，后者则往往是对应的软件名。但这并非绝对，取决于所使用的具体 Docker Registry 的软件或服务。

Docker Registry 公开服务是开放给用户使用、允许用户管理镜像的 Registry 服务，官方的  [Docker Hub](https://hub.docker.com/) 国内访问较慢，Docker 官方和国内很多云服务商都提供了国内加速器服务，比如：

- 阿里云的加速器：https://help.aliyun.com/document_detail/60750.html
- 网易加速器：http://hub-mirror.c.163.com
- Docker官方中国加速器：https://registry.docker-cn.com
- ustc 的镜像：https://docker.mirrors.ustc.edu.cn
- daocloud：https://www.daocloud.io/mirror#accelerator-doc（注册后使用）

当然了，在内部项目中，还可以自己搭建私有的 Docker Registry 服务，官方提供了 [Docker Register](https://hub.docker.com/_/registry/) 镜像。

### Docker 安装

#### 卸载旧 Docker 及依赖

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

#### 安装 Docker CE

1. 安装`docker-ce`

```bash
yum install -y docker-ce
```

2. 设置系统启动

```bash
sudo systemctl start docker
```

3. 检查`docker`状态

```bash
systemctl status docker
```

### Docker 仓库配置

示例使用官方国内镜像仓库地址，对于使用 systemd 的系统，请在 /etc/docker/daemon.json 中写入如下内容（如果文件不存在请新建该文件）

```bash
{"registry-mirrors":["https://registry.docker-cn.com"]}
```

之后重新启动服务

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## Docker 镜像

### 获取镜像

从 Docker 镜像仓库获取镜像的命令是 `docker pull`。其命令格式为：

```bash
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
```

具体的选项可以通过 `docker pull --help` 命令看到，这里我们说一下镜像名称的格式。

- Docker 镜像仓库地址：地址的格式一般是 `<域名/IP>[:端口号]`。如果不指定仓库地址，会使用 Docker 配置的仓库地址，默认地址是 Docker Hub(`docker.io`)。
- 仓库名：如之前所说，这里的仓库名是两段式名称，即 `<用户名>/<软件名>`。对于 Docker Hub，如果不给出用户名，则默认为 `library`，也就是官方镜像。

示例：`docker pull ubuntu:18.04`

```bash
[root@VM-16-13-centos ~]# docker pull ubuntu:18.04
18.04: Pulling from library/ubuntu
40dd5be53814: Pull complete #镜像是分层存储的，前面为每层的 ID 的前 12 位
Digest: sha256:d21b6ba9e19feffa328cb3864316e6918e30acfd55e285b5d3df1d8ca3c7fd3f #镜像完整的 sha256 的摘要
Status: Downloaded newer image for ubuntu:18.04 #下载结果
docker.io/library/ubuntu:18.04 #完整镜像名称
```

### 使用镜像

有了基础镜像之后，可以通过 `docker run`命令基于镜像启动容器，当启动容器时，如果本地不存在该镜像，Docker 还会先从镜像仓库下载该镜像，然后再启动容器，具体的容器相关见 [Docker容器](#Docker-容器)。

### 查看镜像

列举本地已经下载的镜像使用 `docker image ls`命令，其信息包含了 `仓库名`、`标签`、`镜像 ID`、`创建时间` 以及 `所占用的空间`（镜像实际大小，镜像库中的为压缩后的大小）。

```bash
$ docker image ls
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
redis                latest              5f515359c7f8        5 days ago          183 MB
```

可以使用 `docker system df` 命令查询镜像实际占用的大小，不同镜像可能复用了多层存储中的部分层，因此实际占用硬盘大小会小于显示大小。

**虚悬镜像**

有些镜像原本是有镜像名和标签的，随着官方镜像维护，发布了新版本后，重新 `docker pull`时，镜像名被转移到了新下载的镜像身上，而旧的镜像上的这个名称则被取消，标签会变成 `<none>`，这种镜像称为”虚悬镜像“，可以通过`docker image ls -f dangling=true`命令查看虚悬镜像，一般来说，虚悬镜像已经失去了存在的价值，是可以随意删除的。

更多镜像相关命令可通过`docker image ls --help`查看。

### 删除镜像

**删除命令**

如果要删除本地的镜像，可以使用 `docker image rm` 命令，其格式为：

```bash
docker image rm [选项] <镜像1> [<镜像2> ...]
```

其中的镜像可以为`镜像短 ID`、`镜像长 ID`、`镜像名` 或者 `镜像摘要`。

**当镜像删除时，会出现如下几种情况：**

1. 删除的镜像仅有一个标签，命令执行结果显示 `Deleted`，表示删除；
2. 仅删除了某个标签的镜像，此时会看到命令执行结果中，显示的不是 `Deleted` 而是 `Untagged`，因为还有别的标签指向了这个镜像；
3. 删除了一个镜像的全部标签，但是由于镜像是多层存储复用的，可能有别的镜像依赖当前镜像的某一层，依旧不会触发删除该层的行为，也是为什么有时候会发现所删除的层数和自己 `docker pull` 看到的层数不一样的原因；
4. 当删除的镜像有容器依赖其时，需要先删除容器，然后才可以删除镜像。

**镜像删除命令还可以结合镜像查看命令，删除符合查询条件的镜像**

```bash
docker image rm $(docker image ls [选项])
```

### Docker commit

当我们使用一个镜像运行了一个容器，并且进入容器内部进行了修改的时候，可能需要将修改后的镜像保存，`docker commit` 命令可以将容器打包成为一个新的镜像，具体命令格式：

```bash
docker commit [选项] <容器ID或容器名> [<仓库名>[:<标签>]]
```

`docker commit` 虽然可以制作镜像，但是并不推荐使用，如果使用 `docker diff` 命令查询容器的改动后会发现，容器运行后，除了本身的改动外，由于命令的执行，还有很多文件被改动或添加了；另一方面，镜像所使用的分层存储的概念，除当前层外，之前的每一层都是不会发生改变的，换句话说，任何修改的结果仅仅是在当前层进行标记、添加、修改，而不会改动上一层，一次次的 `docker commit` 只会让镜像越来越臃肿，因此更加推荐使用 `dockerfile` 构建镜像。

## Dockerfile

> 镜像的定制实际上就是定制每一层所添加的配置、文件，通常将每一层修改、安装、构建、操作的命令都写入一个脚本，用这个脚本来构建、定制镜像，可以有效解决无法重复的问题、镜像构建透明性的问题、体积的问题，这个脚本就是 Dockerfile。
>
> Dockerfile 是一个文本文件，其内包含了一条条的 **指令(Instruction)**，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。

## Docker 容器

## Docker 仓库

## 参考资料

[Docker从入门到实践](https://vuepress.mirror.docker-practice.com/)