### Docker常用命令

#### 帮助命令

```shell
docker version #显示docker的版本信息
docker info    #显示docker的系统信息，包括镜像和容器数量
docker --help  #帮助命令
```



#### 镜像命令

##### docker images 查看所有本机的主机上的镜像

```shell
[root@jane ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
node          latest    d6740064592f   2 months ago    936MB
hello-world   latest    bf756fb1ae65   14 months ago   13.3kB

#解释
REPOSITORY 镜像的仓库源
TAG        镜像的表情
IMAGE ID   镜像的ID
CREATED    镜像的创建时间
SIZE       镜像的大小

#可选项
 -a, --all     #列出所有镜像
 -q, --quiet   #只显示镜像的id
```



##### docker search  搜索镜像

```shell
docker search node
NAME                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
node                                   Node.js is a JavaScript-based platform for s…   9858      [OK]       
mongo-express                          Web-based MongoDB admin interface, written w…   908       [OK]       
nodered/node-red-docker                Deprecated - older Node-RED Docker images.      353                  [OK]

#可选项
#通过收藏来过滤
 -f=STAR=3000  搜索出来的镜像STAR大于3000的
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output


```



##### docker pull 下载镜像

```shell
#下载镜像 docker pull 镜像名[:tag]
[root@jane /]# docker pull mysql
Using default tag: latest #如果不写tag，默认就是laster
latest: Pulling from library/mysql 
a076a628af6f: Pull complete  #分层下载，docker image的核心 联合文件系统
f6c208f3f991: Pull complete 
88a9455a9165: Pull complete 
406c9b8427c6: Pull complete 
7c88599c0b25: Pull complete 
25b5c6debdaf: Pull complete 
43a5816f1617: Pull complete 
1a8c919e89bf: Pull complete 
9f3cf4bd1a07: Pull complete 
80539cea118d: Pull complete 
201b3cad54ce: Pull complete 
944ba37e1c06: Pull complete 
Digest: sha256:feada149cb8ff54eade1336da7c1d080c4a1c7ed82b5e320efb5beebed85ae8c #签名
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest #真实地址

docker pull mysql
docker pull docker.io/library/mysql:latest #这两个等价于

docker pull mysql:5.7 #指定tag下载



```





##### docker rmi 删除镜像

```shell
[root@jane /]# docker rmi -f c8562eaf9d81 #删除指定的ID
Untagged: mysql:latest
Untagged: mysql@sha256:feada149cb8ff54eade1336da7c1d080c4a1c7ed82b5e320efb5beebed85ae8c
Deleted: sha256:c8562eaf9d81c779cbfc318d6e01b8e6f86907f1d41233268a2ed83b2f34e748
Deleted: sha256:1b649b85960473808c6b812fc30c3f6a3ff1c0ffdcba5c9435daf01cf7d5373a
Deleted: sha256:19cc889447050c16c797fd209fa114ee219de23facb37c00d4137a4ed4aad922
Deleted: sha256:3c793c06a026d276cf56a6a6a75527026ed9eafa7a7d21a438f7d5ed2314148e
Deleted: sha256:1e1cd89a2bc183a7fea3dab0b543e9924278321ad0921c22cc088adbf3c2e77b
Deleted: sha256:83b2015dfd000588c7c947b2d89b3be7a8e5a3abc6ab562668c358033aa779ec
Deleted: sha256:d08533f1e2acc40ad561a46fc6a76b54c739e6b24f077c183c5709e0a6885312
Deleted: sha256:4f9d91a4728e833d1062fb65a792f06e22e425f63824f260c8b5a64b776ddc38
Deleted: sha256:20bf4c759d1b0d0e6286d2145453af4e0e1b7ba3d4efa3b8bce46817ad4109de
Deleted: sha256:a9371bbdf16ac95cc72555c6ad42f79b9f03a82d964fe89d52bdc5f335a5f42a
Deleted: sha256:5b02130e449d94f51e8ff6e5f7d24802246198749ed9eb064631e63833cd8f1d
Deleted: sha256:ab74465b38bc1acb16c23091df32c5b7033ed55783386cb57acae8efff9f4b37
Deleted: sha256:cb42413394c4059335228c137fe884ff3ab8946a014014309676c25e3ac86864

docker rmi -f 镜像Id 镜像id 镜像id #删除多个镜像
docker rmi -f $(docker images -aq) #删除全部的镜像

```



#### 容器命令

说明：我们有了镜像才可以创建容器，linux ，下载一个centos镜像来测试学习

```shell
docker pull centos #下载centos镜像
```

新建容器并启动

```shell
docker run [可选参数] image

#参数说明
--name='name'  跑起来的容器名字
-d             后台方式运行
-it            使用交互方式运行，进入容器查看内容
-p             指定容器的端口  -p 8080:8080
   -p ip：主机端口：容器端口
   -p 主机端口：容器端口 （常用）
   -p 容器端口
   容器端口
-P             随机指定端口

#实践
docker run -it centos /bin/bash  #启动并进入容器
docker run -it --rm tomcat:9:0 #用完即删 一般用来测试
ls #查看容器内的centos，基础版本，很多命令不完善
exit #从容器中退出
ctrl + p + q #容器不停止退出
```

##### 列出所有的运行的容器

```shell
#docker ps命令
docker ps  #列出当前正在运行的容器
docker ps  -a#列出当前正在运行的容器 +带出历史运行过的容器
-n=? #显示最近创建的n哥容器
-q   #只显示容器的编号
-aq  #显示所有容器的编号
```

##### 删除容器

```shell
docker rm 容器id                #删除指定容器，不能删除正在运行的容器，如果要强制删除 rm-f
docker rm -f $(docker ps -aq)  #删除所有容器
docker ps -a -q| xargs docker rm #删除所有容器
```

##### 启动和停止容器的操作

```shell
docker start      #启动容器
docker restart    #重启容器
docker stop       #停止当前正在运行的容器
docker kill       #强制停止当前正在运行的容器
```



#### 常用命令

##### 后台启动容器

```shell
docker run -d centos
#问题docker ps，发现centos停止了

#常见的坑：docker 容器使用后台运行们就必须要有一个前台进程，就必须要有一个前台进程，docker发现没有应用，就会自动停止
#nginx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了
```

##### 查看日志

```shell
docker logs
--tf
--tail num #要显示日志条数
docker logs -f -t --tail 10 3a906faa6421
```

##### 查看容器中进程信息

```shell
#命令 
docker top 容器id
```

##### 查看容器的元数据

```shell
docker inspect 容器id
```

##### 进入当前正在进行的容器

```shell
#我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

#方式一
docker exec -it 容器id bashshell  #进入容器后开启一个新的终端，可以在里面操作（常用）

#方式二 正在执行当前的代码...
docker attach 容器id #进入容器正在执行的终端，不会启动新的进程 

```

##### 从容器内拷贝文件到主机上

 ```shell
docker cp 容器id:容器内路径 目的的主机路径 
 ```

查看cpu的状态

```shell
docker stats
```



### 小结

![image-20210329112103166](C:\Users\huaix\AppData\Roaming\Typora\typora-user-images\image-20210329112103166.png)





