---
title: "Django Notes 12 - User authentication and permissions"
date: 2020-08-26
categories: Django
image: /assets/images/django-logo.png
---
<!--excerpt.start-->
A post to record my learning notes of how to allow users to log in to my site with their own accounts, and how to control what they can do and see based on whether or not they are logged in and their permissions. <!--excerpt.end--> Django comes with an authentication and authorization ("permission") system that provides urls, forms, views we can use directly by importing them. We can write from scratch while for this project, we will use them directly and only to create some templates to show such data. 

# Commands, Files, Packages and Functions 
- django.contrib.auth
- django.contrib.contenttypes 
- django.contrib.sessions.middleware.SessionMiddleware
- django.contrib.auth.middleware.AuthenticationMiddleware

# Enabling authentication
The authentication was enabled automatically when we created the skeleton website. The configuration is set up in the `INSTALLED_APPS` and `MIDDLEWARE` sections of the project file `settings.py`, as shown below: 
 
```py
INSTALLED_APPS = [
    ...
    'django.contrib.auth',  #Core authentication framework and its default models.
    'django.contrib.contenttypes',  #Django content type system (allows permissions to be associated with models).
    ....

MIDDLEWARE = [
    ...
    'django.contrib.sessions.middleware.SessionMiddleware',  #Manages sessions across requests
    ...
    'django.contrib.auth.middleware.AuthenticationMiddleware',  #Associates users with requests using sessions.
    ....
```

# Creating users and groups  
There are many ways to create users ang groups. The easiest way is to use the `admin` site. Login the `admin` site using the `superuser` account info to create some users and groups. Another method is to create users in `python shell`.  

> Note: Only `superuser` has access to admin site and can modify everying of the project. In this project, `groups` of `users` could be library members, librarians, etc and none of them will have the access to the admin site.   

Later, we will add permissions to groups rather than individual users.  

# Setting up your authentication views
Django provides almost everything you need to create authentication pages to handle login, log out, and password management "out of the box". This includes a URL mapper, views and forms, but it does not include the templates so we will create them.  

## Project urls 
We will point django built-in authentication urls to our project urls. Refer to below:
```py
# projectfolder/urls.py
#Add Django site authentication urls (for login, logout, password management)

urlpatterns += [
    path('accounts/', include('django.contrib.auth.urls')),
]
```   

Below is the source code of `django.contrib.auth.urls.py`. Each views inside the `path()` is a Django predefined class-based views located inside `django.contrib.auth/views.py`.
```py
from django.contrib.auth import views
from django.urls import path

urlpatterns = [
    path('login/', views.LoginView.as_view(), name='login'),
    path('logout/', views.LogoutView.as_view(), name='logout'),

    path('password_change/', views.PasswordChangeView.as_view(), name='password_change'),
    path('password_change/done/', views.PasswordChangeDoneView.as_view(), name='password_change_done'),

    path('password_reset/', views.PasswordResetView.as_view(), name='password_reset'),
    path('password_reset/done/', views.PasswordResetDoneView.as_view(), name='password_reset_done'),
    path('reset/<uidb64>/<token>/', views.PasswordResetConfirmView.as_view(), name='password_reset_confirm'),
    path('reset/done/', views.PasswordResetCompleteView.as_view(), name='password_reset_complete'),
]
```
## Template directory
The Functionalities of authentication  will be shared in different apps so it is common to put all templates relates to authentication inside the prpject folder. We then need to tell Django where to find this template directory by adding the `templates` folder directory in `setting.py`. Like below:
```py
# BASE_DIR variable is defined already. 

BASE_DIR = Path(__file__).resolve().parent.parent

TEMPLATES = [
    {
        ...
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
        ...
```  
## Login templage  
We then create a `login.html` inside the `templates` folder. This html can also extend from the base.html. Refer to github repo for template detail. Refer to `forms` post for details on how to understand `forms` in Django. After the template is created, we can go to `http://127.0.0.1:8000/accounts/login` to login as a user. Django will redirect succesfully logged-in users to `http://127.0.0.1:8000/accounts/profile/`, we can change the url by defining `LOGIN_REDIRECT_URL` variable in `setting.py` like below:
```py
LOGIN_REDIRECT_URL = '/'	# redirect to site homepage after succesfull logins
```
## Logout templage  
Refer to github repo for template detail.  
## Password reset templates  
Django by default, sends an email to user to reset their password. Refer to below list of templates to be used at different steps of the password reset process. 
- password_reset_form.html
- password_reset_done.html
- password_reset_email.html
- password_reset_confirm.html
- password_reset_complete.html

# Testing against authenticated users
This testing to exam if a user is logged. If yes, then some information will show; else other information will show. e.g. show "logout" link to logged in user & show "login" link to logged out user. Depending on where is the `is_authenticated` attr saved (either from a class attr or a function parameter), we can test the state in templates, and views respectively.
   
## Testing in templates  
This method is more suitable for check state against class-based views variable. Like the example below, `is_authenticated` is a property of `user` object.   
```py
  <ul class="sidebar-nav">

    ...

   {% if user.is_authenticated %}
     <li>User: {{ user.get_username }}</li>
     <li><a href="{% url 'logout'%}?next={{request.path}}">Logout</a></li>   
   {% else %}
     <li><a href="{% url 'login'%}?next={{request.path}}">Login</a></li>   
   {% endif %} 
  </ul>
```
## Testing in views  
Another method is to check state in views (especially for function-based views). Using `decoator` to extend the function `login_required.`
```py
from django.contrib.auth.decorators import login_required

@login_required
def my_view(request):
    ...
``` 
## To restrict access   
To restrict access to loged_in users in your class-based views is to derive from `LoginRequiredMixin`, like below:
```py
from django.contrib.auth.mixins import LoginRequiredMixin

# only logged in user can call this view
class MyView(LoginRequiredMixin, View):
    login_url = '/login/'
    redirect_field_name = 'redirect_to'
```

# Permissions  
Permissions are associated with models (especially User model) of what permission a user or a group user can do or cannot do. Permissions can assigned to different groups and users in admin site.  By default, Django automatically gives add, change, and delete permissions to all models, which allow users with the permissions to perform the associated actions via the admin site.  
Defining permissions is done on the model `class Meta` section, using the `permissions` field. You can specify as many permissions as you need in a tuple, each permission itself being defined in a nested tuple containing the permission name and permission display value. 
## Models - define permissions  
```py
class BookInstance(models.Model):
    ...
    class Meta:
        ...
        permissions = (("can_mark_returned", "Set book as returned"),)  
```  
## Templates - render something base on permissions  
The current user's permissions are stored in a template variable called {{ perms }}.
```py
{% if perms.catalog.can_mark_returned %}
    <!-- We can mark a BookInstance as returned. -->
    <!-- Perhaps add code to link to a "book return" view here. -->
{% endif %}
```  
## Views - show something based on permissions 
Similar to the login status, Django has different methods to check permissions for function view or class-based views. Refer to below examples:  
Function view decorator: 
```py
from django.contrib.auth.decorators import permission_required

@permission_required('catalog.can_mark_returned')
@permission_required('catalog.can_edit')
def my_view(request):
    ... 


# better version than default 
from django.contrib.auth.decorators import login_required, permission_required

@login_required
@permission_required('catalog.can_mark_returned', raise_exception=True)
def my_view(request):
    ...
``` 
> Note: 
	@permission_required redirects to login screen (HTTP Status 302).
	PermissionRequiredMixin returns 403 (HTTP Status Forbidden). 
When checking is permission is valid, the result should return 403 as more appropriate. So we used @login_required and set the raise_exception=True like the better version.  

A permission-required mixin for class-based views: 
```py
from django.contrib.auth.mixins import PermissionRequiredMixin

class MyView(PermissionRequiredMixin, View):
    permission_required = 'catalog.can_mark_returned'
    # Or multiple permissions
    permission_required = ('catalog.can_mark_returned', 'catalog.can_edit')
    # Note that 'catalog.can_edit' is just an example
    # the catalog application doesn't have such permission!
```


***
Reference:   
1. [Django Tutorial Part 8: User authentication and permissions](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication){:target="\_blank"}  
2. [The Django admin site](https://docs.djangoproject.com/en/3.1/ref/contrib/admin/){:target="\_blank"}  
3. [django LoginView 源码浅析](https://blog.csdn.net/meego17/article/details/77975337){:target="\_blank"}
4. [LOGIN_REDIRECT_URL](https://docs.djangoproject.com/en/3.1/ref/settings/)
5. [Sending email](https://docs.djangoproject.com/en/3.1/topics/email/) 
6. [Limiting access to logged-in users](https://docs.djangoproject.com/en/3.1/topics/auth/default/)  
7. [class property in python](https://docs.python.org/3/library/functions.html#property)



