# Django框架 

### 一、Django简介

#### 1、概述

Django是一个开放源代码的Web应用框架，由Python写成。 在众多的Python Web框架中Django是重量级选手中最有代表性的一位。许多成功的网站和APP都基于Django。



#### 2、入门目标

快速构建简易但完整的web项目，认识MTV结构，熟悉django开发流程。



### 二、Django环境搭建

#### 1、安装Django

- 方式一：`pip install django==2.0.6` （需要外网 -- 推荐使用第一种方式安装）

- 方式二：下载.whl文件 `pip install Django-2.0.6-py3-none-any.whl`

- 方式三：下载压缩包

  下载 Django 压缩包，解压，进入 Django 目录，执行`python setup.py install`，然后开始安装，Django将要被安装到Python的Lib下site-packages。



**检查是否安装成功** 
cmd下进入python环境 ：

```python
import django 

django.VERSION 或 django.get_version()
```



#### 2、虚拟环境搭建

在开发Python应用程序的时候，系统安装了Python3的一个版本：3.5。所有第三方的包都会被pip安装到Python3的site-packages目录下。

如果我们要同时开发多个应用程序，那这些应用程序都会共用一个Python，就是安装在系统的Python 3。如果应用A需要依赖jinja 2.7，而应用B需要依赖jinja 2.6怎么办？

这种情况下，每个应用可能需要各自拥有一套“独立”的Python运行环境。virtualenv就是用来为一个应用创建一套“隔离”的Python运行环境。

**虚拟环境**--在当前主机上的，一个独立于本地环境的一个python运行环境

- 安装virtualenv

```
pip install virtualenv
```

- 创建虚拟环境目录

cmd下进入某个目录，执行：

```
virtualenv TestDemo
```

- 激活虚拟环境

进入TestDemo下的Scripts目录，打开cmd执行

```
activate
```

- 安装依赖库

```
pip install "pillow > 4.3"

pip install "pillow==5"

pip install "Django==2.0.6"

pip install django
```

- 关闭虚拟环境

```
deactivate
```

**注意：**Python3自带了虚拟环境工具pyvenv，类库中增加了一个venv模块：

```
python -m venv  TestDemo
```



### 三、创建Django项目 

#### 1、命令行创建项目

安装 Django 之后，在虚拟环境的Scripts目录下已经有了可用的管理工具 django-admin.py/django-admin.exe。我们可以使用 django-admin 来创建一个项目: ![scripts目录](https://github.com/DeerKing007/Django_learning_notes/blob/master/Django_learning-notes/Django-notes-pic/scripts%E7%9B%AE%E5%BD%95.png)

- 使用 django-admin 来创建 HelloWorld 项目： 

```
django-admin startproject HelloWorld
```

- 进入HelloWorld目录，输入以下命令，启动服务器：

```
python manage.py runserver  
```

- 在浏览器输入你服务器的ip及端口号 

![1531125632678](https://github.com/DeerKing007/Django_learning_notes/blob/master/Django_learning-notes/Django-notes-pic/localhost-server.png)

#### 允许其他浏览器访问：
```
修改settings.py
ALLOWED_HOSTS = ['*']
python manage.py runserver 0.0.0.0:8000
```


#### 2、Pycharm创建项目

- 打开Pycharm，选择【File】->【New Project】->【Django】->【Location】->【Existing interprter】

![Pycharm创建项目](https://github.com/DeerKing007/Django_learning_notes/blob/master/Django_learning-notes/Django-notes-pic/Pycharm创建项目.png)

```
注意：Django在Mac上安装报错找不到manage.py文件时候先执行下面两句命令
python manage.py migrate
python manage.py runserver
```


#### 3、项目目录结构

```
|-- helloworld
	|-- helloworld
	|   |-- __init__.py
	|   |-- settings.py
	|   |-- urls.py
	|   `-- wsgi.py
	`-- manage.py
```

目录说明：

- helloworld: 项目的容器。
  - manage.py:是每个Django项目中自动生成的一个用于管理项目的脚本文件，需要通过python命令执行。 
  - helloworld
    - _ _init_ _.py: 一个空文件，告诉 Python 该目录是一个 Python 包。
    - settings.py: 该 Django 项目的设置/配置。
    - urls.py: 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"。
    - wsgi.py: 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。



#### 4、视图和URL配置

##### 4.1 创建视图

在helloworld/helloworld目录下创建一个views.py文件，并加入以下代码：

```python
from django.http import HttpResponse

def hello(request):
 		return HttpResponse("Hello world ! ")
```

##### 4.2 绑定url

打开urls.py文件，并做如下修改：

```python
from . import view            #引入view模块

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', views.hello),     # view.hello函数 127.0.0.1:8000/hello
]
```

我们使用 django.http.HttpResponse() 来输出"Hello World！"。该方式将数据与视图混合在一起，不符合Django的MVC思想。

##### 4.3 MVC模式

MVC 全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范，用一种业务逻辑、数据、界面显示分离的方法组织代码。 

M是指业务模型，V是指用户界面，C则是控制器，使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。C存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新。 



### 四、模板templates

模板用于分离文档的表现形式和内容。

#### 1、创建templates目录

在helloworld根目录下创建一个templates目录。

#### 2、创建html文件

打开templates目录，并创建一个hello.html文件。

#### 3、添加html内容

在html文件中可以添加如下内容：

```html
<h1>hello</h1>       
```

#### 4、修改settings.py

接下来我们需要向Django说明模板文件的路径，修改helloworld/settings.py，修改 TEMPLATES 中的 DIRS 为 `'DIRS': [os.path.join(BASE_DIR, 'templates')] `，如下所示:

![1531128734303](https://github.com/DeerKing007/Django_learning_notes/blob/master/Django_learning-notes/Django-notes-pic/templates路径设置.png)

#### 5、修改view.py

```python
from django.shortcuts import render,loader     

#加载模板文件
#方式一：loader.get_template()
def hello1(request):
    template = loader.get_template("hello.html")
    return HttpResponse(template.render(request=request))

#方式二：render()函数 更简洁直接
def hello2(request):
    return render(request,'hello.html')   
```

#### 6、MTV模式

Django的MTV模式本质上和MVC是一样的，也是为了各组件间保持松耦合关系，只是定义上有些许不同，Django的MTV分别是值：

- **M 代表模型（Model）：**负责业务对象和数据库的关系映射(ORM)。
- **T 代表模板 (Template)：**负责如何把页面展示给用户(html)。
- **V 代表视图（View）**：负责业务逻辑，并在适当时候调用Model和Template。



### 五、创建APP

project的开发过程中，会有模块化开发，如电商系统中的用户模块，订单模块，OA系统中的财务模块，人力模块等。每个模块都是project的一个APP，APP内是相关模块的功能集合，包含所有相关的功能及完整的实现。将一个project划分为多个APP是一个解耦的过程，整个项目结构松散，利于维护。

- 进入HelloWorld目录，在虚拟环境下执行如下命令：

```
python manage.py startapp firstapp 
                           app名称（模块名称）
```

- App目录结构如下：

```
helloworld
|-- firstapp
|   |-- __init__.py
|   |-- admin.py
|   |-- models.py
|   |-- tests.py
|   `-- views.py
```

- 添加app到settings.py中的INSTALL_APPS中：

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'FirstApp',                        # 新创建的app
]
```

- 在views.py文件中加入如下代码：

```python
from django.shortcuts import render

def hello(request):
    context={}
    context['hello'] = "学习MTV模式"
    return render(request,'hello.html',context)
```

- 修改urls.py

```python
from django.contrib import admin
from django.urls import path

from FirstApp.views import hello    # 引入模块中的hello函数

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/',hello),
]
```



### 六、**虚拟环境补充：**

- **virtualenvwrapper** 是一个基于virtualenv之上的工具，它将所有的虚拟环境统一管理。 

```
pip install virtualenv                  # 安装virtualenv包

pip install virtualenvwrapper-win       # 安装管理虚拟环境的包

# 安装之后配置环境变量
WORKON_HOME=E:\Python Web\Python-Web-Lee\05 Django\Django-Virtual-Env
# 此目录用来统一存放所有创建的虚拟环境  默认目录是：c:\users\用户名\envs

# 创建虚拟环境
mkvirtualenv Test      # 在WORKON_HOME目录下创建名为Test的虚拟环境，且在创建后自己激活虚拟环境
# 后续如果要使用虚拟环境
workon Test

#退出虚拟环境
deactivate 
```

