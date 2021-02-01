---
title: "Django Notes 06 - Forms, Generic Views"
date: 2020-08-20
tags: django
image: /assets/images/django-logo.png
---

# Packages and functions mentioned/used

- Cross Site Request Forgeries
- django.http
  - HttpResponse
  - HttpResponseRedirect
- django.urls
  - reverse()
- HttpRequest
  - request.POST
  - request.GET
- django.views
  - generic
    - generic.ListView
    - generic.DetailView

# Forms
<!--excerpt.start--> 
Form is a very important part of web development and Django can handle form very well. This post is to create a voting form for each poll, submit the form and show the vote results.<!--excerpt.end-->  
The logic is
Step 1: show a vote form on poll detail page
Step 2: submit the form using a post request to vote page - if nothing is voted, then show an error message and remain at the vote page
Step 3: show the vote results on result page

Following the logic, we first need to add a `form` on the `detail.html` template (Step 1).

```py
<form action="{% raw %}{% url 'polls:vote' question.id %}{% endraw %}" method="post">
{% raw %}{% csrf_token %}{% endraw %}
{% raw %}{% for choice in question.choice_set.all %}{% endraw %}
    <input type="radio" name="choice" id="choice{% raw %}{{ forloop.counter }}{% endraw %}" value="{% raw %}{{ choice.id }}{% endraw %}">
    <label for="choice{% raw %}{{ forloop.counter }}{% endraw %}">{% raw %}{{ choice.choice_text }}{% endraw %}</label><br>
{% raw %}{% endfor %}{% endraw %}
<input type="submit" value="Vote">
</form>
```

`action=` defines where will the form date sent to. The value must be a valid url. If value is not valid, then the data will be sent to the page where this form resides.  
`method=` defines if it is `POST` or `GET` method. Submitting a form will alter data server-side so we need to use `method=POST`.  
`csrf_token` is Django's system to protect against Cross Site Request Forgeries. In short, all POST forms that are targeted at internal URLs should use the `csrf_token` template tag.
`for` loop to loops through every choice that a question have. Those choices are retrieved from `question.choice_set.all`.  
`foorloop.counter` variable indicates how many times the for tag has gone through its loop. `foorloop.counter` describes the current iteration of the loop (1-indexed).

The next step is to handle the voting process (Step 2). This is implemented by the `vote()` view function.

```py
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```

> Note: Avoiding race conditions using F()

The last step is to show the vote results on result page. This is implemented by the `results.html` tempalte (Step 3).

# Use generic views: Less code is better

We have used `index()`, `detail()`, `vote()`, `result()` view functions to show data from models so far. These views represent a common case of basic Web development: getting data from the database according to a parameter passed in the URL, loading a template and returning the rendered template. Because this is so common, Django provides a shortcut, called the “generic views” system which uses `Class-based views`. To refactor our code to `Class-based views`, we will:

1. Amend views. Delete some of the old, unneeded views.
2. Amend urls. Convert the URLconf.
3. Amend templates. Introduce new views based on Django’s generic views.
   All code refer to Django tutorial Part 4.

When doing actual project, it is best practice to decide which generic view to use at the beginning.

> Note: Generic view is like some father class. We can create new view by inheriting from them and can also rewrite some methods.

---

Reference:

1. [Django template “pluralize” filter causes raw text output](https://stackoverflow.com/questions/63362950/django-template-pluralize-filter-causes-raw-text-output){:target="\_blank"}
2. [input 标签 name 与 value 的区别](https://blog.csdn.net/houst388/article/details/70821255){:target="\_blank"}
3. [forloop.counter](https://docs.djangoproject.com/en/3.1/ref/templates/builtins/){:target="\_blank"}
4. [Class-based views
   ](https://docs.djangoproject.com/en/3.1/topics/class-based-views/){:target="\_blank"}
5. [Generic display views](https://docs.djangoproject.com/en/3.1/ref/class-based-views/generic-display/){:target="\_blank"}
