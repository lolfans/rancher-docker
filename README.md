1，注册runner
具体参考gitlab以及gitlab-runner的相关操作，网上一大堆。

2，制作基础镜像
具体参考docker镜像的制作和镜像仓库的使用，网上也是一大堆，阿里云账号里面有镜像仓库可以用，dockerhub也可以发布自己的docker镜像，dockerhub与阿里云镜像可以与github设置关联自动构建，即github代码变动，则dockerhub镜像自动根据dockerfile自动构建。

3，编辑Dockerfile以及.env.sandbox
参考制作编写dockerfile的步骤。配置文件都懂得 什么环境用什么配置文件。

4，编辑gitlab-ci.yml
参考gitlabci.yml的编写。作用是根据不同分支或者TAG 构建不同的镜像。测试环境用测试镜像，生产环境用生产镜像。

5，建2个仓库 一个基础镜像仓库一个版本仓库
对于新项目 可以直接在gitlabci里面 通过命令安装三方依赖，老项目迁移则稳妥的办法是将原来的依赖集成到里面。如果后面有新的依赖，也将集成三方依赖的命令加到gitlabci中。

6，提交代码构建推送
推送镜像网上大堆资料。

7，拉取部署测试
部署不需要多言。

-------------------------------------------------------
rancher的搭建参考rancher官网
建议挂载数据库的方式搭建， 方便以后rancher迁移。
rancher拉取镜像的方式很简单。

注意事项有几点：

一，关于rancher 伸缩服务器的时候，如果使用的阿里云的slb或者elb先将要拆的服务器从负载均衡器里面剔除掉，再疏散掉，再删除。否则容易出现服务器被疏散了 ，还有请求往机器上分布，造成事故。

二，一旦有某台服务器重启，建议将该服务器的容器都启动一下。否则队列之类的东西会有问题。

三 第三方例如短信平台，有扩容的服务器 需要将新服务器的IP将 加入鉴权IP白名单。如果是统一出网IP，则只需要该出网IP加入白名单
否则短信验证码会报错 鉴权失败之类的。



