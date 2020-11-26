---
title: "Django Notes 09 - Customize Admin Form"
date: 2020-08-23
categories: Django
image: /assets/images/django-logo.png
---
# Packages and functions mentioned/used 
- django.contrib
	- admin
		- admin.ModelAdmin
			- ModelAdmin.fields
			- ModelAdmin.fieldsets
			- ModelAdmin.inlines
			- ModelAdmin.list_display  
			- ModelAdmin.list_filter
			- ModelAdmin.list_per_page
			- ModelAdmin.search_fields
			- ModelAdmin.date_hierarchy
		- admin.site.register()
		- admin.StackedInline
		- admin.TabularInline


# Admin Form
Django has a default admin layout but if we need to change the admin layout, it will all happen inside the `admin.py` file.  
If we would like to include an interface to interact with the database as `superuser`, we will need to register the model first. 

## Regist models  
```py
# admin.py
admin.site.register(Question)
```

## Create a ModelAdmin subclass  
If we want to change the UI of default admin forms, we will need to create a subclass of `admin.ModelAdmin`.  
```py
# admin.py
class QuestionAdmin(admin.ModelAdmin):
	fields = ['pub_date', 'question_text']
```  
The `ModelAdmin` has many different options. We tried `ModelAdmin.fields`, `ModelAdmin.filedsets`, `ModelAdmin.inlines` to make the interface of the `Question` and `Choice` become more intuitive. For example, to show both question and choices in same page.   

## Add customized filters  
`ModelAdmin` has many options like listed at the beginning. We can add serach box, filter, customized columns/ headers to enhance the UI. 

# Using template on Admin 
We can also use tempalte on the admin site. Django comes with a full set of admin template installed. Built-in admin template location is inside the `Django` package installation folder. Folder structure is like below.  
```
- virtual env -> lib -> python3.8 -> site-packages -> Django
-> contrib -> admin -> templates -> admin -> base_site.html
```  
We can also find all templates for `registration`. 
We will need to create a `templates` folder inside `mysite`; then another folder `admin` inside `mysite/templates/`; finally copy whatever built-in templates we would like to modify into the `mysite/templates/admin/`.

# Customize the admin index page  
By default, Django admin index page displays all the apps in `INSTALLED_APPS` that have been registered with the admin application, in alphabetical order. We can change these by editing the `admin/index.html` template. The `app_list` variable in the `admin/index.html` contains every installed Django app. Instead of using that, we can hard-code links to object-specific admin pages in whatever way we think is best.


***
Reference:   
1. [ModelAdmin objects](https://docs.djangoproject.com/en/3.1/ref/contrib/admin/#django.contrib.admin.ModelAdmin){:target="\_blank"}  
2. [ModelAdmin.fields](https://docs.djangoproject.com/en/3.1/ref/contrib/admin/#django.contrib.admin.ModelAdmin){:target="\_blank"}  