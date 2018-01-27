#	Django
1. [Overview](#overview)

2. [Deployment](#deployment)
	
	2.1 [Requirements](#requirements)
	
	2.2 [Installation](#installation)

<a name="overview"></a>
## 1. Overview

<a name="deployment"></a>
## 2. Deployment
<a name="requirements"></a>
### 2.1 Requirements
- OS: Ubuntu 16.04
- Install: Python 3.5 và Django 1.10

<a name="installation"></a>
### 2.2 Installation
Sử dụng *virtualenv* và *pip* để cài đặt và ở đây tôi sẽ tạo một chương trình *Hello world* đơn giản

* Đầu tiên, tạo ra một thư mục để thực hành bên trong đó

		$ mkdir testapp
		$ cd testapp
		$ virtualenv -p python3 djangotut
		$ djangotut/bin/pip install django
		$ source djangotut/bin/activate

* Tạo một project tên *myproject*

		$ django-admin startproject myproject

ta sẽ được một thư mục *myproject/* như sau

	myproject/
		manage.py
		myproject/
			__init__.py
			settings.py
			urls.py
			wsgi.py

chạy server `python manage.py runserver` và vào http://127.0.0.1:8000/hello/ để xem kết quả

* Tạo một app *hello*
	
		testapp/myproject$ python manage.py startapp hello

sẽ tạo được một thư mục *hello/* 

	hello/
	__init__.py
	    admin.py
	    apps.py
	    migrations/
		__init__.py
		    models.py
		    tests.py
		    views.py

* Sửa file views.py để tạo view đơn giản

		from django.http import HttpResponse

		# Create your views here
		def index(request):
		return HttpResponse("Hello world!")

* Tạo một file *urls.py* trong *hello/* có nội dung như sau:

		from django.conf.urls import url
		from . import views

		urlpatterns = [
		url(r'^$', views.index, name='index'),
		]

* Sửa file *myproject/myproject/urls.py*

		from django.conf.urls import include, url
		from django.contrib import admin

		urlpatterns = [
		    url(r'^hello/', include('hello.urls')),
		    url(r'^admin/', admin.site.urls),
		]

* Chạy server bằng lệnh sau: `python manage.py runserver` sau đó vào xem app của bạn trong http://127.0.0.1:8000/hello/

Nếu muốn thay đổi port hoặc ip thì có thể dùng

	python manage.py runserver your_ip:your_port

hoặc

	python manage.py runserver your_port
