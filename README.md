django-admin startproject mysite


python manage.py runserver

python manage.py runserver 8080

 python manage.py runserver 0:8000

	# starting application name "polls"
python manage.py startapp polls

### configuring polls application ###
# the index page of polls application 
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")

## creating database for polls app 
from django.db import models

# Create your models here.
class Question(models.Model):
    question_text = models.CharField(max_length=100)
    pub_date= models.DateTimeField('date published')

class Choice(models.Model):
    question= models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    vote = models.IntegerField(default=0)

// 
python manage.py makemigrations polls


python manage.py sqlmigrate polls 0001

 python manage.py createsuperuser

## Make the poll app modifiable in the admin�
##  polls/admin.py 


# Create url in polls/urls.py 
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

# mysite/urls 
from django.urls import include, path
from django.contrib import admin

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
# to run server and check 
$ python manage.py runserver
