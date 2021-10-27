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



 
 
 
 

