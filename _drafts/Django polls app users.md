---
---

# Introduction 
This will be a series of posts on how I modify the `polls` step by step to achieve the final goal. This is Part 1, which is to create `users` app and implement the user registration, login & logout functionalities. 

# Packages and Function Mentioned/Used
- python manage.py startapp
- django.contrib.auth.forms 
	- UserCreationForm
- form rendering options 
	-form.as_p
	- form.as_table
	- form.as_ul

# Create Users App
```sh
$ python manage.py startapp users
```
This app resides at the same level of the `polls` app. It is good practice to include app inside `INSTALLED_APP` setting after created. So do not forget. 	

# User Registration From Skeleton 

## Create User Register View 
Next step is to create a `register` view inside `users/views.py`. We used the Django built-in class `UserCreationForm` to create our user register form. 

Step 1: Create an instance of the `UserCreationForm`, name the instance as  `form` .  
Step 2: Create a `context` variable to link the input of the form to the template. 
Step 3: Return a `render()` function.  
```py
def register(request):
    form = UserCreationForm()
    context = {
        'form': form
    }
    return render(request, 'users/register.html', context)
```  

## Plug the View inside a Template  
After we created the view, we will need a template to show the view. The variable `{{ form }}`in the template used to reference to the key of `form` the context inside the `register()` view function. 

## Link Urls  
Consider the project as whole, this registration function is at the same level of the actual polls, so we link `register` url at the project level. So we add a `path()` function inside the `urlpatterns` of `mysite/urls.py`. Do not forget to import the `views` from `users`. 

## Run server
Now we can see a user registration form but the form does not do anything. 

# User Registration From Logic  
## Form Request Method  
Forms have two different methods `GET` or `POST`. In a registration instance, the form method is `POST`. We need to validate form method is `POST` before we handle data in the form. If form method is `GET`, we return the same page. To validate form method, we need to add something in the `register()` view function. 
```py
...
if request.method == 'POST:

```