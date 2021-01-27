后端项目: https://github.com/whitebluepants/giligili-backend



#### 安装模块

```
npm install
```

#### 编译并运行

```
npm run serve
```

#### 编译生产版本

```
npm run build
```



**tips**:

1. 在vue.config.js文件中修改前端对后端api的调用
2. 使用docker生成镜像部署到服务器上
   1. 登录docker, 可以使用阿里云的容器镜像服务, 把镜像推送到阿里云的Docker Registry 
      例子: docker login --username=xxx registry.cn-hongkong.aliyuncs.com
   2. docker build -t "镜像名:版本号" "docker配置文件的目录"  (不带双引号)
   3. docker push "镜像名:版本号" (同上)
3. docker 使用portainer图形化管理容器.