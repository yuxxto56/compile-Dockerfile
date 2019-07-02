![docker_logo](https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3534957911,2629491814&fm=27&gp=0.jpg)
## compile-Dockerfile
编写的简单的dockerfile,了解一下最基础的编译docker镜像文件的源文件书写方式
##  编写代码
* 以apache镜像为例
``` Dockerfile源文件
   # Version 0.1  
   # 镜像基础	
   FROM ubuntu:latest
   # 维护者信息
   MAINTAINER 654516092@qq.com
   # 镜像操作命令
   RUN apt-get -yqq update && apt-get install -yqq apache2 && apt-get clean
   # 容器启动命令
   CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
   
   //备注
   Version 0.1  #标明该镜像的版本,该版本为0.1版本
   FROM ubuntu:latest  #镜像基础源为:ubuntu:latest
   MAINTAINER 654516092@qq.com #书写编写该文件的作者相关信息
   RUN #更新apache必要的扩展库以及安装apache
   CMD #运行容器后，执行的命令，可以理解为执行命令： /usr/sbin/apache2ctl -D FOREGROUND
```
## 编译代码
```complie file
   1、创建编译目录 #根据自己实际的虚拟机|服务器定义
   mkdir /d/wamp/www/apache/
   cd /d/wamp/www/apache/
   2、将上述Dockerfile源文件放入该目录
   3、编译
   docker build -t apache:v1.0 . # apache:v1.0 为镜像源的名称REPOSITORY及TAG,该过程会耗时一段时间，请耐心等待
```
## 运行容器
``` run contanier
   1、查看镜像源
   docker images //会出现如下结果
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   apache              v1.0                6dd854420304        35 minutes ago      187MB
   2、运行容器
   docker run -d -p 8000:80 --name apache apache:v1.0 #指定虚拟机端口8000映射容器端口80
```
## 虚拟机端口映射本机
* 在virtualbox虚拟机环境中查看设置>网络>端口转发中配置如下信息：

名称|协议|主机IP|主机端口|子系统IP|子系统端口
-|-|-|-|-|-|
Rule 2|TCP|127.0.0.1|80|-|8000

## 访问
* 打开浏览器访问：[127.0.0.1](http://127.0.0.1) 即可，显示如下：
![apache-default-page](http://m.qpic.cn/psb?/V1252Obi0sLMks/jrZor*Ikz6e*Zcqr9tqJ5.nUnFLZ2v6ZX3bhqNc1AcM!/b/dDQBAAAAAAAA&bo=JwOXAwAAAAADB5I!&rf=viewer_4)