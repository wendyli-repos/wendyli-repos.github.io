---
title: "Django Notes 03 - Creating a Django App"
date: 2020-08-17
categories: Django
image: /assets/images/django-logo.png
---
# Commands, Files, Packages and Functions 
- python manage.py startapp [appname]
- views.py
	- django.http
		- HttpResponse()
- urls.py
	- django.urls
		- path(route, view [, kwargs, name])
		- include()
	- urlpatterns
	- django.contrib
		- admin.site.urls

# Create the Polls app  
<!--excerpt.start-->First, we need to get the skeleton of an app by create one.<!--excerpt.end-->
1.  `cd` into the same directory as your manage.py file. Type this command to create an app, the app name is `polls`. This will create an app with some files. 
    ```sh
    $ cd [to the project folder]
    $ python manage.py startapp polls
    ```  
> Note: Different between project and app  

To be able to see the app through the browser, we need to have a html page. Django will render `function views`  and/or `classed-based views` reside inside `views.py` to correspondence html. So we need to create a `view`. 
2. Create a view of the `polls` app, open the `polls/views.py` file then added below code.  
	```py
	# polls/views.py
	from django.http import HttpResponse
	
	def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
    ```  
    
Now we have the `view` which is a page. Django needs to know where to find this page by means of `url`. So we need to map this view to a URL. 
3.	To call this view, we will need map it to a URL - and for this we need a `URLconf`. To create a `URLconf` in the polls directory, create a file called `urls.py` and add below code. By doing this, Django knows where to find the `index` page inside the app `polls`. We also need to tell Django where is this `polls` app located inside our `mysite` project, refer to Point 4. 
	```py
	# polls/urls.py
	from django.urls import path
	from . import views

	urlpatterns = [
    	path('', views.index, name='index'),
	]
	```

4.	This step is to include any app level urls to the project level urls. In `mysite/urls.py`, add below code:
	```py
	# mysite/urls.py
	from django.contrib import admin
	from django.urls import include, path

	urlpatterns = [
    	path('polls/', include('polls.urls')),
    	path('admin/', admin.site.urls),
	]
	```
> Note: Can substitue 'polls/' inside the `path()` with any url that is relevant to the site design. 

5.	Activate the server, then visit `http://127.0.0.1:8000/polls/` to view the sentence "Hello, world. You're at the polls index."

***
Reference: 
1. [Writing your first Django app, part 1](https://docs.djangoproject.com/en/3.1/intro/tutorial01/){:target="\_blank"}
2. [django.urls functions for use in URLconfs](https://docs.djangoproject.com/en/3.1/ref/urls/){:target="\_blank"}
3. [Request and response objects](https://docs.djangoproject.com/en/3.1/ref/request-response/){:target="\_blank"}
4. [contrib packages](https://docs.djangoproject.com/en/3.1/ref/contrib/){:target="\_blank"}
