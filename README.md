

注：部署环境为Linux Centos7



## 一、[Docker安装](https://docs.docker.com/install/linux/docker-ce/centos/)



### **方法一**



1、安装前置依赖

```bash

sudo yum install -y yum-utils device-mapper-persistent-data lvm2

```



2、设置阿里软件源

```bash

sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo



sudo yum makecache # 更新

```



3、下载安装

```bash

sudo yum install docker-ce

```



### 方法二



1、下载脚本

```bash

curl -fsSL https://get.docker.com -o get-docker.sh

```



2、执行脚本

```bash

sudo sh get-docker.sh --mirror Aliyun

```



### **配置**



1、开机自启

```bash

sudo systemctl enable docker

```



2、基本命令

```bash

# 启动

sudo systemctl start docker



# 关闭

sudo systemctl stop docker



# 重启

sudo systemctl restart docker

```



3、使用阿里镜像加速

```bash

# 阿里云的容器镜像服务里看镜像加速器地址

sudo mkdir -p /etc/docker 

sudo tee /etc/docker/daemon.json <<-'EOF' { "registry-mirrors": ["https://xxxx.mirror.aliyuncs.com"] } EOF



sudo systemctl daemon-reload

sudo systemctl restart docker

```



## 二、Docker-Compose安装



1、下载docker-compose

```bash

sudo wget https://github.com/docker/compose/releases/download/1.25.0-rc2/docker-compose-Linux-x86_64



mv /path/to/docker-compose-Linux-x86_64 /usr/local/bin/docker-compose

```



2、设置可执行权限

```bash

sudo chmod +x /usr/local/bin/docker-compose

```



3、检测是否安装成功

```bash

docker-compose version

```

## 三、将当前目录下载到目标服务器。

## 四、启动私有仓库服务

进入到部署包根目录下。服务启动在127.0.0.1:4873

```bash

docker-compose up -d

```

注：可能遇到某个文件夹无权限的问题，直接给目录下的storage、log文件夹777权限。



## 六、服务自启

```bash

vim /etc/rc.d/rc.local



# 添加一条

/usr/local/bin/docker-compose -f /path/to/docker-compose.yml up -d



chmod +x /etc/rc.d/rc.local

```



## 七、修改配置

配置文件在conf/config.yaml里，配置修改后要重启服务。

```bash

docker-compose restart

```

