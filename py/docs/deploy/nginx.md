# 简介

> 伊戈尔·赛索耶夫

## 优点

> 高并发量、内存消耗少、简单稳定、模块化程度高、支持Rewrite重写规则、低成本、支持多系统。

## 缺点

> 动态请求处理差、rewrite

# nginx安装

```shell
# ubuntu22.04
# 安装条件
sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring

# 导入官方 nginx 签名密钥，以便 apt 可以验证包的真实性。获取密钥：
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
# 要为稳定的 nginx 软件包设置 apt 存储库，请运行以下命令：
echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
# 设置存储库固定以优先选择我们的包而不是发行版提供的包：
echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
# 安装
sudo apt update && sudo apt install nginx
```

# 启动、停止和重新加载配置

```shell
systemctl start nginx  # 启动
nginx -s stop  # 停止
nginx -s reload  # 修改配置文件之后 重新加载
nginx -t  # 修改配置文件之后 检查
nginx -t -c file.conf  # 检查指定文件
kill -s QUIT 1628 # 杀死进程为1628的nginx服务
ps -ax | grep nginx # 所有正在运行的 nginx 进程的列表
```

# 配置文件的结构

```nginx
/etc/nginx/	  			# root家目录
/etc/nginx/nginx.conf	# Nginx 主配置文件Nginx 启动时会读取 nginx.conf文件
/var/log/nginx			# 日志目录
/var/www/html			# 默认网站目录

# 配置信息简介
全局配置段
http配置段
	server 配置  # 一个server 就是一个web服务，nginx中http配置段下可以用多个server,并且不同server可以监听相同的ip和port
		location 配置
		location 配置
	server 配置
		location 配置
```

## 全局配置块

| 指令     | 说明                                                         |
| -------- | :----------------------------------------------------------- |
| main     | nginx在运行时与具体业务功能（比如http服务或者email服务代理）无关的一些参数，比如工作进程数，运行的身份等。 |
| http     | 与提供http服务相关的一些配置参数。例如：是否使用keepalive，是否使用gzip进行压缩等。 |
| server   | http服务上支持若干虚拟主机。每个虚拟主机一个对应的server配置项，配置项里面包含该虚拟主机相关的配置。在提供mail服务的代理时，也可以建立若干server.每个server通过监听的地址来区分。 |
| location | http服务中，某些特定的URL对应的一系列配置项。                |
| mail     | 实现email相关的SMTP/IMAP/POP3代理时，共享的一些配置项（因为可能实现多个代理，工作在多个监听地址上）。 |

> PID通常是指进程ID（Process ID）。在操作系统中，每个进程都有一个唯一的标识符，即进程ID。PID是用于标识和区分不同进程的数字标签。通过使用PID，操作系统可以对进程进行跟踪和调度，以便对系统资源进行有效的管理和分配。

```nginx
user www-data;			#  设置使用用户
worker_processes auto;  #  子进程 工作进程和cup核数一致或者是它的倍数
pid /run/nginx.pid;     #  服务启动后的进程id  （Process ID）
include /etc/nginx/modules-enabled/*.conf;

# events块用于配置与连接处理相关的参数，主要用来控制Nginx服务器如何处理客户端请求的并发连接。
events {   
	worker_connections 768;  #一个进程允许处理的最大连接数  并发量=进程数*连接数
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
#
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}


存在于http上下文中的指令如下:
    server

    存在于server上下文中的配置指令如下：
        listen
        server_name
        access_log
        location
        protocol
        proxy
        smtp_auth
        xclient

        存在于location上下文中的指令如下：
            index
            root

存在于mail上下文中的指令如下：
    server
    auth_http
    imap_capabilities

存在于main上下文中的配置指令如下:
    user
    worker_processes
    error_log
    events
    http
    mail
```

## HTTP配置块

> `http`块用于配置与HTTP服务器相关的参数和指令

```nginx
server：定义一个虚拟服务器，用于处理特定主机名或IP地址的请求。
listen：指定服务器监听的IP地址和端口号。
server_name：定义服务器的域名或IP地址。
index：指定默认的索引文件。
root：定义服务器的根目录。
include：包含其他配置文件。
proxy_pass：将请求转发到后端服务器。
proxy_set_header：设置转发请求的头部信息。
ssl_certificate：指定SSL证书的位置。
ssl_certificate_key：指定SSL证书的私钥位置。
```

## server配置块

> Nginx的`server`块主要用于配置虚拟主机，即通过监听特定的IP地址和端口来处理来自不同主机的请求。每个`server`块可以配置多个`location`块，用于匹配不同的请求路径和处理方式。

###  `listen`：指定服务器监听的IP地址和端口号。

> 作用：定义Server监听的ip和port，当ip/port匹配时候才进行下一步匹配

表现形式：

| 形式           | 描述                | 示例                  | 完整示例              |
| :------------- | :------------------ | :-------------------- | :-------------------- |
| IP:Port        | 地址精确表示样式    | listen 10.10.10.10:99 | listen 10.10.10.10:99 |
| IP             | 自动监听IP:80地址   | listen 10.10.10.10    | listen 10.10.10.10:80 |
| Port           | 自动监听全地址:Port | listen 99或[::]:99    | listen 0.0.0.0:99     |
| default_server | 自动使用默认的地址  | listen default_server | listen localhost:80   |

> 使用原则：首先将所有样式补全成IP:Port,然后匹配,匹配Server多，那么接着使用Server_name匹配

### `server_name`：定义服务器的域名或IP地址。

> 作用：定义Server监听的域名，当域名匹配时候才进行下一步操作

表现形式：

| 格式 | 完整样式        | 前缀正则样式  | 后缀正则样式  | 禁止非法域名或IP |
| :--- | :-------------- | :------------ | :------------ | :--------------- |
| 形式 | www.example.com | *.example.com | www.example.* | _                |

> 使用原则：优先使用完整样式,然后使用前缀正则样式,最后使用后缀正则样式,如果正则样式相同的时候,匹配最长,否则就走非法规则。非法域名/IP，表示请求到该主机上一个不存在的IP或者域名

### `root`：定义服务器的根目录。

> 作用：定义Server相应请求的html文件所在路径

表现形式：

```
root /var/www/html;
```

### `index`：指定默认的索引文件。

> 作用：定义响应请求后返回的文件名称或格式

表现形式：

```
index index.html index.htm index.nginx-debian.html;
```

### example

```nginx
# 在`/etc/nginx/conf.d`目录下创建server.conf配置文件
server {
    #监听端口
    listen 7000;

    #匹配域名
    server_name 192.168.19.130;

    #根路径
    root /var/www/html;

    #默认显示页面
    index index.html index.htm index.nginx-debian.html;
}

# 检查nginx配置后重载服务
nginx -t
systemctl reload nginx

# 测试访问 
192.168.19.130:7000
```

## location配置块

> ```nginx
> location optional_modifier location_match {
>     # 执行操作...
> }
> # optional_modifier是匹配条件，location_match是匹配的样式，{}是要执行的操作。
> ```

1.**匹配规则**

| 类型        | 含义                   | 匹配方式 | 优先级 | 样式                     |
| :---------- | :--------------------- | :------- | :----- | :----------------------- |
| `=`         | 精确匹配               | 前缀     | 1      | location = /image {}     |
| `^~`        | 优先匹配               | 前缀     | 2      | location ^~ /page {}     |
| `~`         | 普通正则：大小写敏感   | 正则符号 | 3      | location ~ .(jpe?g)$ {}  |
| `~*`        | 普通正则：大小写不敏感 | 正则符号 | 3      | location ~* .(jpe?g)$ {} |
| `空 /`      | 通用匹配               | 前缀     | 4      | location / {}            |
| `空 <路径>` | 前缀匹配               | 前缀     | *      | location /index {}       |

> 优先级：`精确匹配`＞`location 完整路径`＞`优先匹配`＞`正则匹配`＞`location 部分路径`＞`通用匹配`

```nginx
location = / {                     
	# 精确规则A                      
} 

location = /login {      
	# 精确规则B                       
} 

location ^~ /static/ {        
	# 优先规则C                     
} 

location ~ \.(gif|jpg|png|js|css)$ { 
	# 正则规则D
}

location ~* \.png$ {
    # 正则规则E
}

location / {
	# 通用规则F
}

访问 http://a.com/：将匹配规则A
访问 http://a.com/login：将匹配规则B
访问 http://a.com/static/a.html：将匹配规则C
访问 http://a.com/b.png：规则D和E均适合，按顺序优先使用规则D
访问 http://a.com/static/c.png：则优先匹配到规则C
访问 http://a.com/a.PNG：则匹配规则E，因为规则E不区分大小写
访问 http://a.com/category/id/1111：则最终匹配到规则F
```

> `try_files`指令用于尝试按顺序查找文件或目录，并返回找到的第一个存在的文件或目录。它通常用于配置重定向或默认文件处理。

```nginx
location / {
        root   /var/www/html;                    # 指定响应请求的文件所在路径
        index  index.php index.html index.htm;    # 指定响应请求的默认文件名称
        try_files $uri $uri/ =404;                # 如果root指定的路径下有查找的文件，就返回，否则报错
}
```

> root VS alias

```
root和alias所起的作用都是指定响应请求所用文件的路径，只是他们有些许的区别
root 表示location匹配内容的相对路径
alias表示一个绝对路径,而且必须以"/"结尾，否则找不到文件
一般情况下，在location /中配置root，在location /other中配置alias
```

```nginx
demo01：                                         
location /txt/ {
    alias /var/www/txt/;
    index  index.php index.html index.htm;
}                                      
http://localhost/txt/index.html，nginx找/var/www/txt/index.html

demo02：
location /txt/ {
	root /var/www/txt/;
    index  index.php index.html index.htm;
}
http://localhost/txt/index.html，nginx找/var/www/txt/txt/index.html
```

# 反向代理

> ```nginx
> location / {
>  	proxy_pass        http://localhost:8000;    # 设定请求跳转后的地址，可以使用hostname或IP:Port形式
>  	proxy_set_header  X-Real-IP  $remote_addr;  # 后端请求携带原始请求的真实IP地址
> }
> ```

```nginx
server {
    # 监听的端口号
    listen 8001;
    
    # 域名或者ip地址
    server_name 192.168.19.130;
    
    location / {
        # 指向代理
        proxy_pass http://192.168.19.130:8000/;
    }
}
```

# 负载均衡

> 当一台服务器的性能达到极限时，我们可以使用服务器集群来提高网站的整体性能。那么，在服务器集群中，需要有一台服务器充当调度者的角色，用户的所有请求都会首先由它接收，调度者再根据每台服务器的负载情况将请求分配给某一台后端服务器去处理。
>
> 那么在这个过程中，调度者如何合理分配任务，保证所有后端服务器都将性能充分发挥，从而保持服务器集群的整体性能最优，这就是负载均衡问题。

```nginx
upstream backend  {
  server backend1.example.com weight=5;
  server backend2.example.com:8080;
  server unix:/tmp/backend3;
}
 
server {
  location / {
    proxy_pass  http://backend;
  }
}

# upstream 主要是定义一个后端服务地址的集合列表，每个后端服务使用一个server命令表示
# upstream {} 和 Server {} 两部分内容属于平级关系。

```

### upstream配置块

在upstream模块中，可以使用server命令指定后端服务器的地址，同时还可以设置后端服务器在负载均衡调度中的状态，常用的状态有以下几种：

- down： 表示当前server主机暂时不参与负载均衡。
- backup：后备主机，当所有非backup机器出现故障或者繁忙的时候，才会请求backup机器。
- max_fails：允许请求的最大失败数，默认为1，配合fail_timeout一起使用
- fail_timeout：经历max_fails次失败后，暂停服务的时间，默认为10s。

```nginx
# upstream.conf

upstream backends {
	server 192.168.0.101:9999;
	server 192.168.0.101:9998;
	server 192.168.0.101:9997;
}

server {
	listen 10000;
	server_name 192.168.0.101;

	location / {
		proxy_pass http://backends/;
	}
}

python manage.py runserver 192.168.0.101:9999
python manage.py runserver 192.168.0.101:9998
python manage.py runserver 192.168.0.101:9997
```

### Nginx提供的负载均衡策略有两种：

**内置策略：nginx自带的算法**

- 雨露均沾型：轮训、加权轮训、哈希
- 定向服务型：ip_hash、least_conn、cookie、route、lean、
- 商业类型：ntlm、least_time、queue、stick

**扩展策略：各种结合业务场景自定义的算法或者第三方算法**

- 自定义算法
- 第三方算法：fair、url_hash

**常用算法简介：**

- 轮询(默认)：请求按顺序逐一分配到不同的后端服务器。
- weight：指定轮询权重，值越大，分配到的几率就越高，适用于后端服务器性能不均衡情况。
- ip_hash：按访问IP的哈希结果分配请求，分配后访客访问固定后端服务器，有效的解决动态网页会话共享问题。
- fair：基于后端服务器的响应时间来分配请求，响应时间短的优先分配。
- url_hash：按访问URL的哈希结果分配请求，使同URL定向到同一台后端服务器，可提高后端缓存服务器的效率。

```nginx
# 加权轮训实践
#负载均衡
upstream backends {
	server 192.168.0.101:9999 backup;    # 后备主机，当所有非backup机器出现故障或者繁忙的时候，才会请求backup机器
	server 192.168.0.101:9998 weight=1;  # 指定轮询权重，值越大，分配到的几率就越高，适用于后端服务器性能不均衡情况
	server 192.168.0.101:9997 weight=2;
}

server {
	listen 10000;
	server_name 192.168.0.101;

	location / {
		proxy_pass http://backends/;
	}
}

python manage.py runserver 192.168.0.101:9999
python manage.py runserver 192.168.0.101:9998
python manage.py runserver 192.168.0.101:9997
```

```nginx
在 Nginx 中，ip_hash 算法是一种用于确保请求按客户端 IP 地址的顺序进行路由的算法。它的主要目的是防止某些类型的攻击，例如拒绝服务攻击（DoS），其中攻击者可能会使用大量不同的 IP 地址来发起请求，导致服务器过载。

ip_hash 算法的工作原理如下：

当客户端发起请求时，Nginx 会获取客户端的 IP 地址。
Nginx 使用该 IP 地址作为键，在内部数据结构中查找对应的服务器。
如果找到相应的服务器，请求将被路由到该服务器。如果没有找到，请求将被路由到默认的服务器或按照其他策略进行路由。
由于 IP 地址是唯一的，因此每个 IP 地址都将始终被路由到相同的服务器，从而确保来自同一客户端的连续请求都在同一服务器上处理。
这种算法的好处是它可以有效地防止 DoS 攻击，因为攻击者很难通过改变 IP 地址来绕过 ip_hash 算法。然而，它也有一些局限性，例如在高可用性环境中，如果一台服务器出现故障，可能会导致来自同一客户端的请求被路由到不同的服务器上，从而影响用户体验。

总之，ip_hash 算法是一种简单而有效的机制，用于确保来自同一客户端的连续请求被路由到同一服务器上，以防止 DoS 攻击等安全威胁。然而，在某些情况下，它可能不是最佳的选择，需要综合考虑其他因素来选择适合的负载均衡算法。

# ip_hash
upstream backends {
    ip_hash;
    server 192.168.19.130:10086;  
    server 192.168.19.130:10087;  
    server 192.168.19.130:10088 ;
}

server {
    # 监听的端口号
    listen 9001;
    # 服务器
    server_name 192.168.19.130;
    location / {
        # 指向代理
        proxy_pass http://backends/;
    }
}
```

