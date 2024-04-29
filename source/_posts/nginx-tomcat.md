---
title: nginx+tomcat 实现动静分离和负载均衡
link: nginx-tomcat
tags:
  - nginx
  - tomcat
id: '1133'
categories:
  - - 分享
date: 2016-04-02 11:33:05
---

> 动静分离总的来说就是把请求到服务端的动态请求和静态资源的请求分离开，这样在请求量很大的时候能够缓解服务端的压力。之前项目需要用到 nginx 和 tomcat 结合来实现动静分离和负载均衡，在这里整理一下做为总结。

## 动静分离原理

服务端接收来自客户端的请求中，有一部分是静态资源的请求，例如html,css,js和图片资源等等，有一部分是动态数据的请求。因为tomcat处理静态资源的速度比较慢，所以我们可以考虑把所有静态资源独立开来，交给处理静态资源更快的服务器例如nginx处理，而把动态请求交给tomcat处理。 如下图所示(图画的有点丑，将就着看看)，我们在机器上同时安装了nginx和tomcat,把所有的静态资源都放置在nginx的webroot目录下面，把动态请求的程序都放在tomcat的webroot目录下面，当客户端访问服务端的时候，如果是静态资源的请求，就直接到nginx的webroot目录下面获取资源，如果是动态资源的请求，nginx利用反向代理的原理，把请求转发给tomcat进行处理，这样就实现了动静分离，提高了服务器处理请求的性能。 [![b0d887aacf05b3b5ea74018b66a6039c989668c3](http://vsnote.test/wp-content/uploads/2016/04/b0d887aacf05b3b5ea74018b66a6039c989668c3.png)](http://vsnote.test/wp-content/uploads/2016/04/b0d887aacf05b3b5ea74018b66a6039c989668c3.png)

## 动静分离的实现

_注：本文是在 centos-6.5 64 位操作系统搭建的_

### 环境安装

首先下载 jdk、tomcat 和 nginx 的安装包，可到各大官网下载，这里我的jdk用的是1.7版本，tomcat 用的是8.0版本，nginx 用的是1.7.7版本。

###  jdk 安装

//解压到 /usr/local/java/目录
# tar -zxvf jdk-7u67-linux-x64.tar.gz －C /usr/local/java/
//配置环境变量
# vi /etc/profile

在最后加入以下几行：

JAVA\_HOME=/usr/java/jdk1.7.0\_71
CLASS\_PATH=.:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar    
PATH=$JAVA\_HOME/bin:$PATH                                      
export JAVA\_HOME CLASS\_PATH PATH

执行下面命令立即生效

\# source /etc/profile

tomcat 安装

\# tar zxvf apache-tomcat-7.0.29.tar.gz  -C /usr/local/tomcat/

tomcat 安装后不用做配置，但是要测试是否能跑起来，这里不做过多的描述 nginx 安装

//在nginx包的目录解压nginx,可解压缩到任意目录，这里解压缩到当前目录
# tar zxvf nginx-1.7.7.tar.gz                    
//进入nginx-1.7.7目录，进行编译                    
# cd nginx-1.7.7                                  
# ./configure --prefix=/usr/loacl/nginx/          
# make && make install

nginx需要编译，所以发现无法编译，那么可能是机器没有安装编译环境，需要安装编译环境，执行如下命令：

yum -y install gcc gcc-c++ autoconf automake
yum -y install zlib zlib-devel openssl openssl-devel pcre-devel

## 配置动静分离

这里主要是配置 nginx 的nginx.conf 文件,nginx 的配置可以参考网上其他资料，这里不做详细描述。 进入 /usr/local/nginx/conf/ 目录，编辑 nginx.conf 文件

\# cd /usr/local/nginx/conf/                   
# vi nginx.conf

这里我们主要修改的是http模块里面的server节点，其他配置不用改，配置如下:

server {
        listen       80;                       
        server\_name  127.0.0.1;               
        root  /usr/local/html/;
        index  index.html index.htm index.jsp;

        charset koi8-r;

        access\_log  logs/host.access.log  main;

        location ~ \\.(jsp)$ {
           proxy\_pass http://www.tomcat.com:8080;
           proxy\_redirect off;
           proxy\_set\_header HOST $host;
           proxy\_set\_header X-Real-IP $remote\_addr;
           proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;
           client\_max\_body\_size 10m;
           client\_body\_buffer\_size 128k;
           proxy\_connect\_timeout 90;
           proxy\_send\_timeout 90;
           proxy\_read\_timeout 90;
           proxy\_buffer\_size 4k;
           proxy\_buffers 4 32k;
           proxy\_busy\_buffers\_size 64k;
           proxy\_temp\_file\_write\_size 64k;
        }

        location ~ \\.(gifjpgpngbmpswfhtmljscsshtm)$
        {
         expires 10d;
        }
 }

其中 listen 表示nginx监听的端口，server\_name是nginx对外提供访问的ip或者域名，root是nginx存放资源的路径。 下面的两个 location 节点就是动静分离的配置了，location有下面6种匹配方式：

*   \=：精确匹配
*   空修饰符且精确匹配
*   ^~：匹配前面
*   ~：使用正则表达式匹配，大小写敏感
*   ~\*：使用正则表达式匹配，大小写不敏感，和4没有高低之分
*   空修饰符且前面匹配

这里我们用第4种 ～ ，使用正则表达式，并且大小写敏感，第一个 location 表示以 .jsp 结尾的请求，我们利用反向代理的方式，把请求转发给tomcat进行处理，其中 proxy\_pass 需要配置tomcat的ip。我们也可以配置restful api形式的请求，例如我们想把请求接口的 url 里面带有字母 a 的请求转发给 tomcat 进行处理，我们可以配置 location ~ a 即可。 第二个location表示以 .gif .jpg .js 等结尾的请求，我们直接到nginx的root目录里面获取资源，这定义用户浏览器缓存的时间为10天，如果静态页面不常更新，可以设置更长，这样可以节省带宽和缓解服务器的压力。 至此，我们已经配置好动静分离了，启动nginx和tomcat就可以了。

## 负载均衡的实现

配置好动静分离，那么负责负载也就很简单了。负载均衡就是将 tomcat 的动态请求分摊到多个 tomcat 执行，这个在请求量很大的时候能缓解服务端的压力，主要的配置是在 nginx.conf 的配置文件的http节点里面添加 upstream 节点，如下：

upstream tomcats{                               
    server 10.11.68.56:8080 weight=1;     
    server 10.11.68.57:8080 weight=1;       
    server 10.11.68.58:8080 weight=1;     
}
server {
    listen       80;                       
    server\_name  172.24.69.127;                
    root  /usr/local/html/;  
    index  index.html index.htm index.jsp;

    location / {
       proxy\_pass http://tomcats;
       proxy\_redirect off;
       proxy\_set\_header HOST $host;
       proxy\_set\_header X-Real-IP $remote\_addr;
       proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;
       client\_max\_body\_size 10m;
       client\_body\_buffer\_size 128k;
       proxy\_connect\_timeout 90;
       proxy\_send\_timeout 90;
       proxy\_read\_timeout 90;
       proxy\_buffer\_size 4k;
       proxy\_buffers 4 32k;
       proxy\_busy\_buffers\_size 64k;
       proxy\_temp\_file\_write\_size 64k;
    }
}

其中，upstream 节点里面配置的是每个参与负载均衡的tomcat的ip, weigth 参数表示权值，权值越高被分配到的几率越大,如果每台机器的weight=1,表示每台机器被分配到的概率是一样的。tomcats是upstream配置项的名称，可以自定义，但是一定要和locatin节点里面的 proxy\_pass 配置一样 至此，我们已经把动静分离和负载均衡配置好了。 文章来源：[Nginx+tomcat实现动静分离和负载均衡](http://139.196.14.76/t/nginx-tomcat/260)