---
title: "Django Notes 01 - Installing Django In Virtual Environment, Requirements.txt"
date: 2020-08-15
tags: django
image: /assets/images/python-venv.png
---

<!--excerpt.start-->Django is a Python package, so we need to install before we can use it. It is preferred to install Django in a python virtual environment. <!--excerpt.end-->Below are notes of how to. 
 
# Create Python venv in VS Code and install Django
There are two sections of the procedure. First section [Step 1 - 5] is to set up a python virtual environment and install `Django` in this virtual environment. Second section [Step 6 - 9] is to create a `Django` project (e.g. like a blog project, website project, poll project, etc.); then run the server to check if everything is okay.

1.  Create a project folder, where the virtual env and Django project will reside. such as `django_project`.
2.  `cd` into `django_project`, then to create a virtual environment named `django_env` inside `django_project` by running below command.

    ```sh
    $ cd django_project
    $ sudo apt-get install python3-venv # If needed
    $ python3 -m venv django_env
    ```

3.  `cd` into `django_env` to install Django. There are two methods.  
    Method 1: In VS Code, choose the installed virtual environment `django_env` as the python interpreter, then open a new bunit-in terminal, then install Django as Step 4.  
    Method 2: In Mac terminal, active the installed virtual environment first, then install Django as Step 4.

    ```sh
    $ cd django_env
    $ source bin/activate
    ```

4.  Install Django in the virtual environment by running.

    ```sh
    $ pip install django
    ```
> Note: Because this is only a demo project so I can just install Django. In real project, there maybe many packages needed to install. And Python has a shortcut to install all packages in one `pip` command, refer to below section [What about requirements.txt](#What about requirements.txt). 
5.  Check if Django is installed successfully. If returns Django version then means installation is completed.

    ```sh
    $ python -m pip install django
    ```

6.  To create a django project inside the `django_project` folder; `django_blog_project` is the project name, after this command is executed, a django_blog_project will be created, refer to next section. 

    ```sh
    # make sure virtual env is activated
    # make sure you are in the `django_project` folder
    $ cd django_project
    $ django-admin startproject django_blog_project
    ```

7.  To run server; ensure to run this command in the manage.py directory.

    ```sh
    $ cd django_blog_project
    $ python manage.py runserver
    ```

8.	A localhost server will run and usually you can visit `http://127.0.0.1:8000/` to check if a django welcome page shows.  

9.	To stop the server, press `Control` + `C` on Mac.

10. To deactivate virtual environment in Mac terminal.
    `$ deactivate`  

# What about requirements.txt 
One way to install Django is as Point 4 above, the other shortcut is to install all packages and dependencies using the `requirements.txt` file. 

# Create a requirements.txt  
There are two ways to create `requirements.txt` file. 

Method 1: To just create a text file named `requirements` at the same level of the virtual env. And put all packages and dependencies inside this text file. Something similar to below if Django is the only package to install at the time. 
```text
Django~=2.2.4
```  
Then run below command inside the venv and Django 2.2.4 will be installed. 
```sh
$ pip3 install -r requirements.txt
``` 
Method 2 (preferred): The ultimate purpose of requirements.txt is to easily install all packages and dependencies on different machines. Python has a command to create `requirements.txt` automatically based on your current installations. This is usually done when the project is ready for publishment. Refer to below:
```sh
$ pip3 freeze > requirements.txt.
```    
It is best practice to include a `requirements.txt` when publishing the project. 

 
***
Reference: 
1. [Django Tutorial in Visual Studio Code](https://code.visualstudio.com/docs/python/tutorial-django){:target="\_blank"}
