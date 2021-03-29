

### 镜像是什么





### Docker镜像加载原理

#### 联合文件系统 

分层下载



### 分层理解



docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部

这一层就是我们通常说的容器层，容器之下的都叫镜像层

![image-20210329170037368](C:\Users\huaix\AppData\Roaming\Typora\typora-user-images\image-20210329170037368.png)



### commit镜像

```shell
docker commit 提交容器成为一个新的副本

#命令和git原理类似
docker commit -m '提交的描述信息' -a="作者" 容器id 目标镜像名:[TAG]
```

- 如果你想要保存当前容器的状态，就可以通过commit来提交，获得一个镜像