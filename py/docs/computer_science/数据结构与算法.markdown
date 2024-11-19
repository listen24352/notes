# 部署Django

```shell
# 查看Linux系统版本
lsb_release -a

Distributor ID: Ubuntu
Description:    Ubuntu 22.04.5 LTS
Release:        22.04
Codename:       jammy
```

## python环境搭建

```shell
sudo apt -y install python-is-python3 python3.10-venv python3-pip

# 创建虚拟环境
cd ~
mkdir .vnev
cd .venv
python -m venv web
. ./web/bin/activate

# 安装Python依赖包
pip install -r requirements.txt
```

## gunicorn

```python
# 配置gunicorn
pip install gunicorn

# 创建Gunicorn服务文件
sudo vim /etc/systemd/system/gunicorn.service

# 添加内容
[Unit]  
Description=gunicorn daemon  
After=network.target  

[Service]  
User=leo
Group=leo  
WorkingDirectory=/home/leo/Desktop/thesis/bec  
ExecStart=/home/leo/.venv/web/bin/gunicorn --workers 3 --bind unix:/tmp/192.168.68.130.socket bec.wsgi:application  

[Install]  
WantedBy=multi-user.target




sudo systemctl daemon-reload  
sudo systemctl start gunicorn  
sudo systemctl enable gunicorn

# 重新加载systemd并启动Gunicorn服务

Warning: The unit file, source configuration file or drop-ins of gunicorn.service changed on disk. Run 'systemctl daemon-reload' to reload units.
警告:gunicorn的单元文件、源配置文件或插件。磁盘上的服务已更改。运行'systemctl daemon-reload'重新加载单元。

Created symlink /etc/systemd/system/multi-user.target.wants/gunicorn.service → /etc/systemd/system/gunicorn.service.

```

## nginx

```python
sudo vim /etc/nginx/sites-available/192.168.68.130

server {  
    listen 80;  
    server_name 192.168.68.130;  

    location = /favicon.ico { access_log off; log_not_found off;}  
    location /static/ {  
        alias /home/leo/Desktop/thesis/bec;  
    }  

    location / {  
        include proxy_params;
        proxy_pass http://unix:/tmp/192.168.68.130.socket;
    }  
}

```

```
sudo ln -s /etc/nginx/sites-available/192.168.68.130 /etc/nginx/sites-enabled
```

```
sudo systemctl status gunicorn
sudo systemctl status nginx
```

