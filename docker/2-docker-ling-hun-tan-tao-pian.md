作业大纲:

```
01 Dockerfile实战
    通过Dockerfile，将自己的项目build成image镜像，并且根据image创建对应的container，最后能够成功访问，
    不妨将步骤和截图发出来秀一下。
02 docker commit实战
    不妨下载一个官方的镜像，然后创建container，对该container进行修改，然后再commit成自己的镜像，最后根据自己的镜像创建容器。
03 准备自己的阿里云镜像仓库
    根据上课和笔记的学习，拥有自己的一个阿里云容器镜像仓库，并且可以将前面的image push到阿里云容器镜像仓库中，方便后面学习和使用。
04 搭建容器搭建平台weavescope
```

## 1 使用 Dockerfile 文件创建自己的 image

\[1\] 想法是: 创建一个简单的 spring-boot 项目, 将这个项目打成 jar 包, 然后根据这个 jar 包, 构建自己的 image, 并在容器中跑起来.

\[2\] 具体的步骤:

\(0\) 上传 jar 包到 centos 系统:

```
1) 我是通过 FileZilla 软件将 jar 从 win10 上传到 VMWare 的 192.168.119.131
2) 然后通过 scp root@192.168.119.131:/opt/tmp/*.jar ./  将 jar 包远程拷贝到本地的;
```

\(1\) 拼写 Dockerfile 文件:

\(2\) 构建 image 文件:

\(3\) 运行 images 文件:

\(4\) 访问对应的接口: /hello-world

## 2 使用 docker commit 创建 image 文件:

## 3 搭建 阿里云 的 docker image 仓库:

## 4 使用 weasescope 搭建监控平台:

---



