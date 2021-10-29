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
    11111
 2. detached模式下的交互<br/>
    docker exec -it ID/ImageName sh
    
    
    
 
 

 




 
 
 
 

