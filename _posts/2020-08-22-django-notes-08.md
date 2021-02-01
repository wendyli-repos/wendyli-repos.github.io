---
title: "Django Notes 08 - Adding static files"
date: 2020-08-22
tags: django
image: /assets/images/django-logo.png
---
<!--excerpt.start-->
A post to record my learning notes of how to adding static files to a Django app. <!--excerpt.end-->

# Packages and functions mentioned/used 
- django.contrib.staticfiles
	- finders.AppDirectoriesFinder
- STATICFILES_FINDERS setting


# Adding static folders to the app  
Create a `static` folder inside the `polls`, like `template` folder. 
```css
# polls/static/polls/style.css
li a {
    color: green;
}
```  
The below code added a `style.css` to the `index.html` template.
```py
# polls/templates/polls/index.html
{% raw %}{% load static %}{% endraw %}

<link rel="stylesheet" type="text/css" href="{% raw %}{% static 'polls/style.css' %}{% endraw %}">
```  

# Adding images to the app  
Similar to `style` folder. 
```css
# polls/static/polls/style.css
body {
    background: white url("images/background.gif") no-repeat;
}
``` 

# Adding framework (to be edited)
# Staticfiles reference (to be edited)
# Deploying static files (to be edited)


***
Reference:   
1. [django ORM双下划线汇总](https://blog.csdn.net/qq_19691995/article/details/102395469){:target="\_blank"}  
