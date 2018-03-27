
话不多说，整体架构如下：

用户通过DNS解析Elastic Load Balancer的URL，ELB转发请求到其中任何一台Word Press的EC2实例；

该Web Server通过3309端口访问远程的MySQL RDS实例；

MySQL通过Multiple-AZ实现高可用；Web Server通过ELB实现高可用；

根据CPU或者其他负荷标准，ELB里面可以自动增加，删除EC2实例；

Auto Scaling 创建的服务器必须自动更新到最新版本；

所有的图片和视频保存在S3 Bucket上面，并通过CloudFront实现CDN加速，博客的媒体资源URL自动重定向指向CDN的地址进行解析。
