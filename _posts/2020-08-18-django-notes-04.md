---
title: "Django Notes 04 - Setup Database"
date: 2020-08-18
categories: Django
image: /assets/images/django-logo.png
# permalink: /:categories/:title
---
# Packages and functions used 
- django.http
	- HttpResponse()
- django.urls
	- path(route, view [, kwargs, name])
	- include()
- django.contrib
	- admin()

# Create the Polls app  
1.  `cd` into the same directory as your manage.py file. Type this command to create an app, the app name is `pools`.  
    ```
    $ cd [to the project folder]
    $ python manage.py startapp polls
    ```  
> Note: Different between project and app  
2. Write a view of the `polls` app, open the polls/views.py file then added below code.  
	```
	from django.http import HttpResponse
	
	def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
    ```
3.	To call this view, we will need map it to a URL - and for this we need a URLconf. To create a URLconf in the polls directory, create a file called urls.py.  
	```
	from django.urls import path
	from . import views

	urlpatterns = [
    	path('', views.index, name='index'),
	]
	```
4.	The next step is to point the root URLconf at the polls.urls module. [Namely to include any urls inside an app to the project that the app resides.] In mysite/urls.py, add an import for django.urls.include and insert an include() in the urlpatterns list, so you have:
	```
	from django.contrib import admin
	from django.urls import include, path

	urlpatterns = [
    	path('polls/', include('polls.urls')),
    	path('admin/', admin.site.urls),
	]
	```
> Note: Can substitue 'polls/' inside the `path()` with any url that is relevant to the site design. 

5.	Activate the server, then visit `http://127.0.0.1:8000/polls/` to view the sentence "Hello, world. You're at the polls index."


Reference: [Writing your first Django app, part 1](https://docs.djangoproject.com/en/3.1/intro/tutorial01/){:target="\_blank"}
