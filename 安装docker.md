

```sh
# 查看linux版本
uname -r
3.10.0-693.2.2.el7.x86_64
```

```sh
# 系统版本 
cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

安装

```shell
# 1.卸载旧的docker
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
# 2.需要的安装包
yum install -y yum-utils

# 3.设置镜像的仓库
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo #默认是从国外的
    
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo #阿里云镜像仓库

# 更新yum软件包索引
yum makecache fast

# 4.安装docker docker-ce 社区版 ee企业版
yum install docker-ce docker-ce-cli containerd.io

#5.启动docker
systemctl start docker

#6.运行docker
docker run hello-world

#7.查看docker版本
docker version

#8.查看一下下载的这个 hello-world镜像
docker images
    
```

查看docker版本

![查看docker版本](C:\Users\huaix\AppData\Roaming\Typora\typora-user-images\image-20210326151634857.png)



运行docker helloworld

![image-20210326151828569](C:\Users\huaix\AppData\Roaming\Typora\typora-user-images\image-20210326151828569.png)