### Ubuntu 20.04 上部署 Django

#### Ubuntu 20.04 Django uWSGI Nginx

为部署项目准备
```shell
sudo apt-get install git mysql-server nginx
```
为安装uWSGI准备
```shell
sudo apt-get install python3-dev build-essential
```
为Python3虚拟环境准备
```shell
sudo apt-get install python3-venv
```
为安装mysqlclient（Python 包）准备
```shell
sudo apt-get install default-libmysqlclient-dev
```

### 上传项目，创建Python虚拟环境，进入虚拟环境

更新 pip，下载 uWSGI
```shell
pip install -U pip setuptools uwsgi
```

准备数据库
```sql
# 创建数据库
create database 5x5x5_plan;
# 为数据库创建用户
CREATE USER '5x5x5_plan'@'%' IDENTIFIED WITH caching_sha2_password BY '12345678';
# 为创建的用户，赋上对创建数据库的权限
GRANT ALL PRIVILEGES on 5x5x5_plan.* TO '5x5x5_plan'@'%';
# 刷新权限
FLUSH PRIVILEGES;

show variables like 'validate_password%';

SELECT user,authentication_string,plugin,host FROM mysql.user;

```

uWSGI 配置
```ini
[uwsgi]

project = plan_5x5x5
base = /home/ubuntu/plan_5x5x5


module = %(project).wsgi:application
# 静态文件挂载，--static-map mountpoint=path
# static-map = /static=static


# 开启一个主进程，管理其他进程
master = true
# 设置进程， processes 和 workers 一样
# processes = 2
workers = 4
# 每个进程的线程数
threads = 4


socket = %(base)/uWSGI/socket_%(project).socket
chmod-socket=666

# uwsig pid 路径
pidfile = %(base)/uWSGI/pid_%(project).pid

# 未使用 systemd 时日志文件，会一直保持在后台，使用 docker 应该使用 logto
# daemonize = %(base)/uWSGI/log_%(project).log
# 使用 systemd 时 日志文件
logto = %(base)/uWSGI/log_%(project).log

# 服务停止时，自动移除unix socket和pid文件
vacuum = true

```

Nginx 配置
```conf
server {
    listen 80;
    charset utf-8;

    client_max_body_size 75M;

    location /static {
        alias /home/ubuntu/plan_5x5x5/static;
    }

    location / {
        uwsgi_pass unix:/home/ubuntu/plan_5x5x5/uWSGI/socket_plan_5x5x5.socket;
        include /etc/nginx/uwsgi_params;
    }
}
```

Systemd(systemctl) 配置
```ini
[Unit]
Description=plan_5x5x5
After=network.target

[Service]
WorkingDirectory=/home/ubuntu/plan_5x5x5
ExecStart=/home/ubuntu/plan_5x5x5/venv/bin/uwsgi --ini /home/ubuntu/plan_5x5x5/plan_5x5x5_uwsgi.ini
ExecStop=/home/ubuntu/plan_5x5x5/venv/bin/uwsgi --stop /home/ubuntu/plan_5x5x5/uWSGI/pid_plan_5x5x5.pid
ExecReload=/home/ubuntu/plan_5x5x5/venv/bin/uwsgi --reload /home/ubuntu/plan_5x5x5/uWSGI/pid_plan_5x5x5.pid

[Install]
WantedBy=multi-user.target

```

参考链接：
- [uWSGI项目](https://uwsgi-docs-zh.readthedocs.io/zh_CN/latest/index.html)
- [Nginx中文文档](https://www.nginx.cn/doc/)
- [ubuntu部署python專案(virtualenv + flask + uwsgi + nginx)](https://www.itread01.com/content/1546097282.html)
- [【Python 教学】uWSGI 配置参数讲解](https://www.maxlist.xyz/2020/06/20/flask-uwsgi/)
- [centos7 systemctl 添加 uwsgi（开机启动）](http://www.xieboke.net/article/383/)
- [plan_5x5x5_uwsgi.ini](Django_uWSGI_Nginx_files/plan_5x5x5_uwsgi.ini)
- [plan_5x5x5_uwsgi.service](Django_uWSGI_Nginx_files/plan_5x5x5_uwsgi.service)
- [mysite_nginx.conf](Django_uWSGI_Nginx_files/mysite_nginx.conf)
- [mysite_uwsgi.ini](Django_uWSGI_Nginx_files/mysite_uwsgi.ini)
- [tmp_uwsgi.ini](Django_uWSGI_Nginx_files/tmp_uwsgi.ini)
