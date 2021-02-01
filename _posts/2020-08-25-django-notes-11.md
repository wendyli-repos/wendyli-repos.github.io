---
title: "Django Notes 11 - Deploy Django on Heroku"
date: 2020-08-25
tags: django
image: /assets/images/django-logo.png
---
<!--excerpt.start-->
A post to record my learning notes of how to deploy a Django app using Heroku. <!--excerpt.end-->

# Get Heroku Prepared
1.	Create a Heroku account   
2.	Install Heroku CLI. To check if Heroku is installed, type below in the terminal.  
```sh
$ heroku```  
3.	Install Git as Heroku uses git to upload all local files to Heroku. After git is installed, add a `.gitignore` file in the root directory, for content of the `.gitignore` file, refer to [this repo](https://github.com/wendyli-repos/code-snippets-django).  
	Initiate a git repo at the root directory; add, commit then push procedure.   
```sh
$ git init
$ git add .
$ git commit -m "some messages"
$ git push Heroku master
```
4.	Install `gunicorn`
5.	Install `dj-database-url` and update settings.py, refer to [this snippet](https://github.com/wendyli-repos/code-snippets-django/blob/main/settings.DATABASES).
6.	Install `whitenoise` to handle static files.

# Get Some Files Ready for Heroku
1.	Procfile 
2.	requirements.txt
3.	(optional) runtime.txt. If not provided, Heroku will install bu default.

# Set Variables  
Below are some variables to be edited in settings.py, refer to [here](https://github.com/wendyli-repos/code-snippets-django)  
1.	SECRTET_KEY
2.	DEBUG
3.	ALLOWED_HOSTS
4.	STATIC_ROOT, STATICFILES_STORAGE
5.	MIDDLEWARE
6.	DATABASES
7.	LOGGING

# Start deployment 
1.	Login Heroku  
```sh
$ heroku login``` 
2.	Create Heroku app   
```sh
$ heroku create <app-name>``` 
3.	Initiate git; & add and commit; & push local files to Heroku  
```sh
$ git push heroku master```  
4. Setting Heroku config    
```sh
$ heroku config:set SECRET_KEY=''
$ heroku config:set DEBUG=''
$ heroku config:set EMAIL=''
$ heroku config:set AWS=''
$ ...
```  
5. Visit site   
```sh
$ heroku open
```

# Some useful Heroku commands  
1.	Run shell inside Heroku  
```sh
$ heroku run python manage.py shell
```
2. Run bash inside Heroku  
```sh
$ heroku run python mange.py bash
```


***   
Reference: 
1. [Getting Started on Heroku with Python](https://devcenter.heroku.com/articles/getting-started-with-python#set-up) {:target="\_blank"}
