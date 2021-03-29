## Docker 架构

![查看源图像](https://th.bing.com/th/id/Rcfdb56686b86ab77daec52830fdad3da?rik=OwxDWNSQI1ROCg&pid=ImgRaw)

##### 镜像（image）

docker镜像就好比是一个模板，可以通过这个模板来创建容器服务，tomcat镜像===>run===>tomcat1容器（提供服务器），通过这个镜像可以创建多个容器（最终服务运行或者项目运行就在这个容器中的）

##### 容器（container）

docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的

启动，停止，删除，基本命令！

目前就可以把这个容器理解为就是一个建议的linux系统，项目

##### 仓库(repository)

仓库就是存放镜像的地方！

仓库分为公有仓库和私有仓库

docker Hub（默认是国外的）

阿里云...都有容器服务器（配置镜像加速）



