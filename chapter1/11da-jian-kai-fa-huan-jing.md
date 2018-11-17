## 安装虚拟环境

pip install virtualenv

---

## 创建虚拟环境

virtualenv \[path\]虚拟环境名

---

## 安装Django

* 安装

```
pip install django
```

* 查看版本

```
import django
django.get_version()

“”“
>>> import django
>>> django.get_version()
'2.0.5'
“”“
```

---

## 创建项目

* 使用命令创建test1文件夹

```
django-admin startproject test1
```

* test1目录结构图

![](/assets/django目录结构图.png)

---

## 目录文件说明

* manage.py:一个命令行工具，能够使用多种方式对Django项目进行交互
* 内层的目录:项目的真正的python包
* \__init\_\_.py:一个空文件，告知python这个目录应被看作python包\_
* setting.py:项目的配置
* urls.py:项目的URL声明
* wsgi.py:项目与WSGI兼容的Web服务器入口



