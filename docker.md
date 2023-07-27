教程地址:
https://juejin.cn/post/6844903946234904583

安装docker咯
```
1.在项目文件夹下新建Dockerfile文件(设计蓝图)
# 基础镜像为node，版本为v9.2.0
FROM node:9.2.0

# 创建容器内的项目存放目录
RUN mkdir -p /home/nodeapp
WORKDIR /home/nodeapp

#  将Dockerfile当前目录下所有文件拷贝至容器内项目目录并安装项目依赖
COPY . .
RUN npm install

# 容器对外暴露的端口号，要和node项目配置的端口号一致
EXPOSE 3000

# 容器启动时执行的命令
CMD [ "node", "app.js" ]


2.构建镜像
docker build -t my-node-image .

3.运行容器
docker run -d --name my-node-container -p 3000:3000 my-node-image

-d表示容器会在后台运行；--name 是我们给容器起的名字，这个名字是唯一的；-p表示端口映射，即将容器内的3000端口映射到宿主机器的3000端口上，这样外部就可以通过80端口来访问容器内部运行的应用了。
```

## 更新容器脚本update.sh 
```
#!/bin/bash
# 停止和删除旧的容器
docker stop my-node-container
docker rm my-node-container
docker rmi my-node-image

# 重新构建和运行容器
docker build -t my-node-image .
docker run -d --name my-node-container -p 3000:3000 my-node-image
```


拉取Node镜像
示例:docker pull node:9.2.0

##查看容器状态
docker ps -a

##进入容器
1.
docker exec -it 容器名 /bin/bash
docker exec -it 容器名 cmd

2.
镜像是使用alpine制作的，要进入该容器需要输入
docker exec -it 容器名 /bin/sh
