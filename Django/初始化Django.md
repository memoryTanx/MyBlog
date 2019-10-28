#### 搭建 Django 项目环境

0. 首先确定有没有模块 venv，没有则安装：pip install --user virtualenv
1. 创建虚拟环境：python -m venv venv
2. 激活虚拟环境：venv\Scripts\activate    退出虚拟环境：deactivate
3. 安装 Django：pip install django
4. 创建项目： django-admin startproject Django1 .
5. 同步数据库：python manage.py migrate
6. 运行：python manage.py runserver 8000
7. 创建应用程序：python manage.py startapp login
8. 创建迁移文件：python manage.py makemigrations login
9. 同步数据库：python manage.py migrate
10. 创建超级用户：python manage.py createsuperuser

