---
title: "Django Notes 07 - Automated Testing"
date: 2020-08-21
tags: django
image: /assets/images/django-logo.png
--- 
<!--excerpt.start-->
A post to record my learning notes of how to test a Django app. <!--excerpt.end-->

# Packages and functions mentioned/used 
- datetime
	- datetime.timedelta()
- django.utils
	- timezone
		-timezone.now()
- django.test
	- TestCase
	- Client
		- Client()
			- client.get()
- django.test.utils
	- setup_test_environment()
- response.status_code
- response.content
- response.context
- Question.objects.order_by()
- Question.objects.create()
- Question.objects.filter()
- get_queryset()
	- timezone
		- timezone.now()
- pub_date__lte	
- assertIs()
- assertEqual()
- assertContains()
- assertQuerysetEqual()

# Automated testing in Django  
## Location to save test cases  
A conventional place for an application’s tests is in the application’s `tests.py` file. 
 
## Naming convention for test case  
1. Create a subclass of the `TestCase` Class.
2. Create a test method with the name starting with `test` + `a descriptive name of the method`. In the test method, we should include the setup of a test database. 
3. the testing system will automatically find tests in any file whose name begins with test.  

## Run test by this command  
```sh
$ python manage.py test polls
```  

We can also test a `view`. Django provides a test C`lient` to simulate a user interacting with the code at the view level. We can use it in `tests.py` or even in the `shell`.

# The Django test client
```sh
>>> from django.test import Client
>>> # create an instance of the client for our use
>>> client = Client()
```

***
Reference:   
1. [django ORM双下划线汇总](https://blog.csdn.net/qq_19691995/article/details/102395469){:target="\_blank"}  
