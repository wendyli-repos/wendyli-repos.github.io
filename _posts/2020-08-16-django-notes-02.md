---
title: "Django Notes 02 - Django 'MVC"
date: 2020-08-16
tags: django
image: /assets/images/django-logo.png
---

# Django Structure
## The model layer ("M" of the "MVC")  
Django provides an abstraction layer (the “models”) for structuring and manipulating data of your Web application. Models can create databases.   

## The view layer ("V" of the "MVC")  
Django has the concept of “views” to encapsulate the logic responsible for processing a user’s request and for returning the response with a relevant view (which could be extended from a tempalte.) 

### The template layer 
The template layer provides a designer-friendly syntax for rendering the information to be presented to the user.  

### Froms  
Django provides a rich framework to facilitate the creation of forms and the manipulation of form data.  

## The control layer ("V" of the "MVC")
### urls.py
The developer to point Django to go to which url to show a view. 

***
Reference: 
1. [Django documentation](https://docs.djangoproject.com/en/3.1/){:target="\_blank"}
