
话不多说，整体架构如下：

用户通过DNS解析Elastic Load Balancer的URL，ELB转发请求到其中任何一台Word Press的EC2实例；

该Web Server通过3309端口访问远程的MySQL RDS实例；

MySQL通过Multiple-AZ实现高可用；Web Server通过ELB实现高可用；

根据CPU或者其他负荷标准，ELB里面可以自动增加，删除EC2实例；

Auto Scaling 创建的服务器必须自动更新到最新版本；

所有的图片和视频保存在S3 Bucket上面，并通过CloudFront实现CDN加速，博客的媒体资源URL自动重定向指向CDN的地址进行解析。

现在我们开始具体的配置，会配置一个Ubuntu16.04 LTS 的WordPress。服务器和MySQL数据库都具有高可用的功能，还可以通过CPU的负荷自动添加或者删除现有实例。具体的配置包括以下步骤：

创建基本的网络和防火墙

配置高可用MySQL

创建一个Ubuntu 14实例

Ubuntu安装LAMPStack

配置S3和CloudFront CDN

配置Ubuntu Virtual Host

配置Route 53 DNS 

测试通过之后配置成AMI镜像

配置ELB

配置Auto scaling

测试
