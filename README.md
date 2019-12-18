# Start
Python web project

1)<ініціаліація джанго в нововуму проекті>

    django-admin startproject main

    cd main/

    python manage.py migrate

    python manage.py createsuperuser



2)<створити  папку(firstapp) з апкою>

    python manage.py startapp firstapp



3)підключити свою апку до проекту

settings - INSTALLED_APPS = ['django.contrib.admin', 'firstapp']


4) в папці апки створюємо файл urls.py
заповняємо в нього

from django.urls import path
from .views import hello, wtf

urlpatterns = [
    path('hello/', hello),

]

5)в папці апки файл views.py створюємо функцію

from django.http import HttpResponse

def hello(request):
    return HttpResponse('hello world')

def wtf(request):
    return HttpResponse('what the fuck???')

6)в початковій папці main - urls
додаємо шлях до firstapp - urls


urlpatterns = [
    path('admin/', admin.site.urls),
    path('admin/', include('firstapp.urls'))
]


7) path('test/<int:gift_id>/', test)

def test(request, gift_id):
    return HttpResponse(f'Gift id - {gift_id}')


8)myapp - models

from django.db import models

class Dog(models.Model):
    name = models.CharField(max_length=100, null=False)
    age = models.IntegerField()
    breed = models.CharField(max_length=20)



python manage.py makemigrations
python manage.py migrate

9)myapp - admin

from .models import Dog

admin.site.register(Dog)










1) створити папку темплейтс а в ній хтмл файл

підключити його

main - settings - TEMPLATES

'DIRS': [os.path.join(BASE_DIR, 'templates')],


2)


myapp - urls

path('topics/', topics),


myapp - views

def topics(request):
    topics = Topic.objects.filter().first()

    return render(request, 'index.html',
    {
        'topic_name': topics.title,
        'text': topics.body
    })


html

        <h2>{{topic_name}}</h2>

        <p>{{text}}</p>



myapp - views


def topics(request):
    tops = Topic.objects.all()

    return render(request, 'index.html',
    {
        'tops': tops
    })


html


        {% for topic in topics %}

            <h2>{{ topic.title }}</h2>

        {% endfor %}
















