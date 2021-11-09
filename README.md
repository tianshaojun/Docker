# Docker

### 1.wins下安装docker

111

### 2.linux下安装docker
 
 1. 使用curl命令下载shell脚本<br/>
    curl -fsSL get.docker.com -o get-docker.sh
 2. 使用sh命令执行这个脚本<br/>
    sh get-docker.sh
 3. 检查是否安装成功<br/>
    docker version
 4. 开启docker服务端<br/>
    sudo systemctl start docker

### 3.创建容器相关命令

> 镜像像是一个包含了OS文件系统和应用的对象，类似虚拟机的模板(比如Windows10镜像)。可以把镜像看成面向对象编程中的只读类(read-only Class)。

> 容器和镜像几乎一模一样，唯一的区别是镜像是只读的，而容器上面有一个可读写层。所以容器=镜像+读写层。

镜像和容器区别

![](https://github.com/tianshaojun/Docker/blob/master/img/01.jpg)

 1. 创建一个容器<br/>
    docker container run nginx
 2. 查看容器的信息和状态<br/>
    docker container ls<br/>
    docker container ps(不建议使用)
 3. 停止正在运行容器<br/>
    docker container stop name/ID
 4. 查看所有容器，包含已经停止容器<br/>
    docker container ls -a
 5. 删除容器<br/>
    docker container rm name/ID

相关命令简写方法

![](https://github.com/tianshaojun/Docker/blob/master/img/02.png)

### 4.多容器操作和强制删除容器的方法

 1. 查看所有容器的ID<br/>
    docker container ps -aq
 2. 停止多个容器<br/>
    docker container stop $(docker container ps -aq)
 3. 删除多个容器<br/>
    docker container rm $(docker container ps -aq)
 4. 强制删除容器<br/>
    docker container rm ID/ImageName -f

### 5.attached 和 detached 模式

 1. docker 端口映射,让Docker可以被访问到<br/>
    docker container run -p 80:80 nginx(第一个端口是映射到服务器本机的端口，第二个端口是Docker容器使用的端口)
 2. 开启detached模式<br/>
    docker run -d -p 80:80 nginx
 3. detached模式转换为attached模式<br/>
    docker attach  ID/ImageName
 
### 6.detached模式下查看logs
 
 1. 查看日志<br/>
    docker container logs ID/ImageName
 2. 跟踪日志<br/>
    docker container logs -f ID/ImageName
    
### 7.Docker的交互式模式

 1. 使用Ubuntu镜像并开启交互模式<br/>
    docker container run -it ubuntu sh<br/>
    -it 代表启用交互模式<br/>
    sh 代表使用Shell脚本<br/>
    ls  得到目录下的文件<br/>
    hostname  查看计算机名称<br/>
    exit  退出容器和交互模式<br/>
 2. detached模式下的交互<br/>
    docker exec -it ID/ImageName sh<br/>
    exec  执行<br/>
    -it  交互模式<br/>
    sh  用shell脚本进行交互<br/>
    ls  得到目录下的文件<br/>
    exit  退出容器和交互模式<br/>
    
### 8.镜像获取和Image Registry

 1. 获取镜像的三个基本途径：
    + 从网络社区直接拉取
    + 从Dockerfile构建一个镜像
    + 自有文件的导入，可以从本地导入已经构建好的镜像文件，在没有网络的时候可以用
 2. 镜像社区介绍：<br/>
    + dockerhub   https://hub.docker.com/
    + Quay   https://quay.io/

### 9.Image镜像的拉取和删除

 1. 镜像的所有命令和提示<br/>
    docker image
 2. 从dockerhub上拉取镜像<br/>
    docker image pull wordpress
 3. 拉取具体版本号镜像<br/>
    docker pull wordpress:php7.3-fpm-alpine
 4. 从Quay.io上拉取镜像<br/>
    docker pull quay.io/calico/node
 5. 查看镜像列表的方法<br/>
    docker image ls
 6. 查看镜像具体信息<br/>
    docker image inspect ImageID
 7. 删除镜像<br/>
    docker image rm ImageID

### 10.镜像的导入导出
  1. 导出镜像<br/>
     docker image save busybox:latest -o mybusybox.image
  2. 导入镜像<br/>
     docker image load -i mybusybox.image
     
### 11.初识Dockerfile

> Docker是一个包含用于组合映像的命令的文本文档。可以使用在命令行中调用任何命令。Docker通过读取Dockerfile中的指令自动生成映像。

  1. Dockerfile是用于构建docker镜像的文件<br/>
  2. Dockerfile里包含了构建镜像所需的"指令"<br/>
  3. Dockerfile有其特定的语法规则<br/>
  
### 12.通过Dockerfile构建镜像

  1. Dockerfile构建镜像<br/>
     docker image build -t jspang .
  2. 执行容器<br/>
     docker run jspang
     
### 13.把镜像分享到Dockerhub

  1. 符合社区规则的镜像创建<br/>
     docker image build -t jspangcom/jspang .<br/>
     docker image tag oldImageName newImageName
  2. 登录dockerhub<br/>
     docker login
  3. 把镜像push到社区<br/>
     docker image push jspangcom/jspang
     
### 14.FROM语法和镜像选择
 
  选择基础镜像的三个原则：<br/>
  1. 官方镜像优于非官方的镜像<br/>
  2. 固定版本的Tag，而不是每次都使用latest<br/>
  3. 功能满足，选择体积小的镜像<br/>

### 15.RUN执行指令使用技巧

  1. Dockerfile打包命令<br/>
     docker image build -f Dockerfile.bad -t ipinfo-bad .<br/>
  2. 查看具体分层情况<br/>
     docker image history ImageID
     
### 16.Dockerfile中的文件操作

  1. 用copy命令构建镜像<br/>
     docker image build -f Dockerfile.copy -t hello-copy .<br/>
  2. 用add构建镜像<br/>
     docker image build -f Dockerfile.add -t hello-gzip .<br/>
  3. 切换工作目录workdir
     
### 17.Dockerfile中的ARG和ENV

  1. ARG是构建环境，ENV可带到镜像中<br/>
  2. ARG可以在构建镜像时改变变量值
  
### 18.CMD容器启动命令

  1. 批量删除已经退出的容器<br/>
     docker system prune -f
  2. 删除没有使用的所有镜像<br/>
     docker image prune -a
  3. CMD命令的三个基本特性：<br/>
     + 容器启动时默认执行的命令
     + 如果docker container run 启动容器时指定了其他命令，则CMD命令会被忽略
     + 如果定义多个CMD，只有最后一个CMD执行
  4. 容器启动时指定命令<br/>
     docker container run -it ipinfo-base ipinfo version
  
### 19.ENTERPOINT命令的使用

ENTRYPOINT和CMD的区别：<br/>
  1. CMD设置的命令，可以在docker container run时传入其他命令，覆盖掉CMD的命令，但是ENTRYPOINT所设置的命令时一定会被执行的。<br/>
  2. ENTRYPOINT和CMD可以联合使用，ENTRYPOINT设置执行的命令，CMD传递参数。

### 20.VOLUME命令设置数据持久化-1

  1. 查看所有的持久化空间(主要是存储空间的ID)<br/>
     dokcer volume ls
  2. 查看持久化的具体地址<br/>
     docker volume inspect id
     
 ### 21.VOLUME命令设置数据持久化-2
 
  1. 给volume起名字，实现复用<br/>
     docker container run -d -v my-data:/app my-image
 
  ### 22.Bind Mount实现数据持久化
  
  1. Bind Mount命令的使用<br/>
     docker container run -it -v ${pwd}:/app node
     
     












     
     
     
     
    
