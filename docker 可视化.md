## 可视化

- portainer
- Rancher(CI/CD再用)



##### 什么是portainer？

Docker图形化界面管理工具！提供一个后台面板供我们操作！

```shell
docker run -d -p 8080:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true --name prtainer  portainer/portainer
```



 