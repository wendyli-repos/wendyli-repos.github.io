---
title: "Django Notes 04 - Database, Timezone, Models, Admin"
date: 2020-08-18
categories: Django
image: /assets/images/django-logo.png
---
# Packages and functions mentioned/used 
- DATABASES
- TIME_ZONE
- makemigrations
- sqlmigrate
- migrate
- django.db
	- models
	- models.Model
	- models.CharField()
	- models.DateTimeField()
	- models.ForeignKey()
	- models.IntegerField()
- datatime
- django.utils
	- timezone
- django.contrib 
	- admin
	- admin.site.register()

# Modify setting.py   
1.	Change `DATABASE` used if needed. Default db is SQLite.  
2. 	Change `TIME_ZONE` if needed. Default timezone is 'UTC'.  
3.	Adding the `polls` app inside `INSTALLED_APPS` by adding below line. `PollsConfig` is found inside the `app.py` file inside the app folder.  
	```py
	'polls.apps.PollsConfig',
	```
	
# SQlite CLI 
1.  `cd` into the directory where there is a `db.sqlite3` file. This file is a SQLite database file. Type this command to enter into the `sqlite>` prompt.  
    ```sh
    $ cd [to the folder where db.sqlite3 resides]
    $ sqlite3
    $ sqlite>			# terminal will prompt this
    $ sqlite> .schema	# to view database 
    ```  
2.	Press `Control` + `D` to exit 

# Create models (databases) in Django
1.	Edit the polls/models.py file so it looks like this:
	```py
	from django.db import models

	class Question(models.Model):
    	question_text = models.CharField(max_length=200)
    	pub_date = models.DateTimeField('date published')

	class Choice(models.Model):
    	question = models.ForeignKey(Question, on_delete=models.CASCADE)
    	choice_text = models.CharField(max_length=200)
    	votes = models.IntegerField(default=0)
	```
> Note: each model is represented by a class that subclasses django.db.models.Model
> Note: Each field is represented by an instance of a Field class – e.g., CharField for character fields and DateTimeField for datetimes. This tells Django what type of data each field holds.

2. Create correspondence databases [the purpose of this command is like a pre-process of the database queries] 
	```sh
	$ python manage.py makemigrations polls
	```
	
3.	To review what migrations have completed as SQLite queries. 
	```sh
	$ python manage.py sqlmigrate polls 0001
	```
> Note: Good habit to run the above after makemigrations to ensure SQL queries are as what  they are intended to do.  

4.	Tips: can also run below to check if any problems.
	```sh
	$ python manage.py sqlmigrate polls 0001
	```  
	
5. 	Create Database  
	```sh
	$ python manage.py migrate
	```  

# Playing with the API  
Inside the shell, I can access object properties, refer to this link [Related objects reference](https://docs.djangoproject.com/en/3.1/ref/models/relations/)
1.	Start a Python interactive shell  
	```sh
	$ python manage.py shell
	```
	
2.	Exit the shell by pressing `Control` + `D`  

# Django Admin  
1.	Create an admin user  
	```sh
	$ python manage.py createsuperuser
	```  
2.	Follow prompts to set `username`, `email` and `password`.  
3.	Run server then visit `.../admin/` to log into the admin portal.
4.	After login `Admin` portal, the `superuser` can edit databases. But before that, databases will need to register in `polls/admin.py` file.  
	```py
	from .models import Question
	from .models import Choice

	admin.site.register(Question)
	admin.site.register(Choice)
	```

***
Reference:   
1. [how-to-set-the-timezone-in-django](https://stackoverflow.com/questions/29311354/how-to-set-the-timezone-in-django){:target="\_blank"}
