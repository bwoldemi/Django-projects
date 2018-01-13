# This documents guides step by step creating a django project ###
### creating project mysite
`django-admin startproject mysite`

### check the created project running the server, the default port is 8000
python manage.py runserver

### to run the server in port  other than the defalut port. 
python manage.py runserver 8080

### to run the server in a certain ip address 
 python manage.py runserver 0:8000

# Creating application name: polls 
python manage.py startapp polls

### configuring polls application
### on views.py create a method index which handles the view 

from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
    
### To create a URLconf in the polls directory, create a file called urls.py under polls directory: 

from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

#  In mysite/urls.py, add an import for django.urls.include and include url file 

from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path('', include('user.urls')),
    path('admin/', admin.site.urls),
]


# Creating database for polls app 
from django.db import models

### Create your models here.
class Question(models.Model):
    question_text = models.CharField(max_length=100)
    pub_date= models.DateTimeField('date published')

class Choice(models.Model):
    question= models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    vote = models.IntegerField(default=0)

## commit the following command to create the database and the models 
python manage.py makemigrations polls
python manage.py sqlmigrate polls 0001

# Crating the supper user 
python manage.py createsuperuser

# Make the poll app modifiable in the admin¶
##  polls/admin.py 
