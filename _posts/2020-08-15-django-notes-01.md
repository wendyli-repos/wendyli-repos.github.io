---
title: "Django Notes 01 - Setting up Django environment"
date: 2020-08-15
categories: Django
# permalink: /:categories/:title
---

### Create Python venv in VS Code and install Django

1.  Create a project folder, such as `django_project`.
2.  `cd` into `django_project`, create a virtual environment named `django_env` by running below command.

    ```
    $ sudo apt-get install python3-venv # If needed
    $ python3 -m venv django_env
    ```

3.  `cd` into `django_env` to install Django. There are two methods.  
    Method 1: In VS Code, choose the installed virtual environment `django_env` as the python interpreter, then open a new bunit-in terminal, then install Django as Step 4.  
    Method 2: In Mac terminal, active the installed virtual environment first, then install Django as Step 4.

    ```
    $ cd django_env
    $ source bin/activate
    ```

4.  Install Django in the virtual environment by running.

    ```
    $ pip install django
    ```

5.  Check if Django is installed successfully. If returns Django version then means installation is completed.

    ```
    $ python -m pip install django
    ```

6.  To create a django project; `django_project` is the project name, after this command is executed, a django_project will be created, refer to next section.

    ```
    $ django-admin startproject django_project
    ```

7.  To run server; ensure to run this command in the manage.py directory.

    ```
    $ python manage.py runserver
    ```

8.  To deactivate virtual environment in Mac terminal.
    `$ deactivate`

Reference: [Django Tutorial in Visual Studio Code](https://code.visualstudio.com/docs/python/tutorial-django){:target="\_blank"}
