---
title: "Django Notes 05 - Views, Templates, 404 Errors, Urls"
date: 2020-08-19
categories: Django
image: /assets/images/django-logo.png
permalink: /:categories/:title
---
# Packages and functions mentioned/used 
- URL dispatcher
- ROOT_URLCONF setting
- TEMPLATES setting
- django.template
	- loader
- django.shortcuts
	- render(request object, tempalte name, context)
	- get_object_or_404(django model, kwags)
	- get_list_or_404()_
- get() method of the model's manager
- filter() method of the model's manager
	- HttpResponse
	- Http404



# What is `views`?  
In Django, web pages and other content are delivered by views. Each view is represented by a Python function (or method, in the case of class-based views). Django will choose a view by examining the URL that’s requested (to be precise, the part of the URL after the domain name).  
   
   
# How to show views?  
Every view function (or method) will need to be wired to `urls.py` to show. Inside `urls.py`, adding path() of each view as an element of the `urlpatterns` list. The procedure is to load a template -> fill a context -> return an HttpResponse. As it is so common that Django provided a shortcut render() function to handle this procedure.    

> Note: The `%s` inside the string is a placeholder, indicating that whatever after the `%` will replace the `%s` inside the string.  


# The basic purpose of views  
Each view is responsible for doing one of two things: returning an `HttpResponse` object containing the content for the requested page, or raising an exception such as `Http404`. The rest is up to you.  
> Note: View can do anything using different libraires; but each view must have return HttpResponse. Or an exception.  


# Generate different views using templates  
1.	Create a `templates` folder inside the app folder `mysite/polls/`.  
2. 	Create a `polls` folder inside `mysite/polls/tempaltes`.
3. 	Create an `index.html` inside `mysite/polls/tempaltes/polls/`. This html file will be rendered as the `template` of `index view`. Using DTL (similar to `Liquid`) to create the html template like below. 
	```
	# mysite/polls/tempaltes/polls/index.html
	{% if latest_question_list %}
        <ul>
            {% for q in latest_question_list %}
                <li><a href="/polls/{{ q.id }}/">{{q.pub_date}} | {{ q.question_text }}</a></li>
            {% endfor %}
        </ul>
    {% else %}
        <p>No polls are available.</p>
    {% endif %}
	```
> Note: The 'latest_question_list' variable in the above template references to the `key` of the `context` dictionary defined inside the `index view` function.   
4.	The below code loads the template called `polls/index.html` and passes it a `context`. The `context` is a dictionary mapping template variable names to Python objects. 
	```
	# views.py - return HttpResponse syntax
	def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
	```  
The above can be rewritten using `render()`. The `render()` function takes the request object as its first argument, a template name as its second argument and a dictionary as its optional third argument. 
It returns an HttpResponse object of the given template rendered with the given context.  
	```
	# views.py - render() syntax
	def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
	```

# Raising a 404 error  
Inside each view function, we should handle `404 error` before render the correspondence template.  
	```
	def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    context = {'question': question}
    return render(request, 'polls/detail.html', context)
	```
The above code can be rewritten using `get_object_or_404()`  
	```
	def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    context = {'question': question}
    return render(request, 'polls/detail.html', context)
	```
> Note: The name of get_object_or_404() is quite self-explanatory. If can get the object or a 404. object here means models class.

# More about template  
To show data from different tables using foreign keys. Edited the `detail.html` template as per below.  
```
<h1>{{ question.question_text }}</h1>
	<ul>
	{% for choice in question.choice_set.all %}
    	<li>{{ choice.choice_text }}</li>
	{% endfor %}
</ul>
```  
The `question.choice_set` returns an iterable of `Choice` objects correspondencing to `Question` via a foreign key. The naming convention by Django is `foo_set`, this can be renamed using `related_name` attribute inside the `class Choice()` like below.
	```
	class Choice(models.Model):
    question = models.ForeignKey(
        Question, on_delete=models.CASCADE, related_name='choices')
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
	```  

# Remove hardcoded url in template  
Using the `{% url %}` template tag to replace hardcoded urls inside tempalte. 
	```
	# hardcode urls like "/polls/{{ q.id }}"
	<!-- <li><a href="/polls/{{ q.id }}/">{{q.pub_date}} | {{ q.question_text }}</a></li> -->
    
    # replaced with {%  url 'name of the path' %}
    <li><a href="{% url 'detail' q.id %}">{{q.pub_date}} | {{ q.question_text }}</a></li>
      ```

# Namespacing URL names  
To differentiate the URL names between different apps. Adding `app_name` before `urlpatterns` inside `urls.py`.  
	```
	# polls/urls.py
	app_name = 'polls'
	```  
Then to prefix the `{% url 'detail' question.id %}` to `{% url 'polls:detail' question.id %}`. 

***
Reference:   
1. [Templates](https://docs.djangoproject.com/en/3.1/topics/templates/#:~:text=Django%20ships%20built%2Din%20backends,for%20the%20popular%20alternative%20Jinja2.){:target="\_blank"}  
2. [Playing with Context objects](https://docs.djangoproject.com/en/3.1/ref/templates/api/#playing-with-context){:target="\_blank"}
3. [Methods that do not return QuerySets](https://docs.djangoproject.com/en/3.1/ref/models/querysets/#django.db.models.query.QuerySet.get){:target="\_blank"}
4. [python - Django教程中的choice_set.all是什么
](https://www.coder.work/article/365574){:target="\_blank"}
5. [Django教程：什么是choice_set？](https://cloud.tencent.com/developer/ask/81697){:target="\_blank"}