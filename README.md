# Полная последовательность подготовки проекта Django

## Подготовка
```bash
python --version
pip --version
git --version
```

# 1. Поднятие проекта
## 1.1 Создай папку проекта
```bash
cd C:\Users\efimz\Desktop
mkdir abilympics_festival
cd abilympics_festival
```

## 1.2 Создай виртуальное окружение
```bash
python -m venv venv
```

## 1.3 Активируй его
```bash
.\venv\Scripts\Activate.ps1
```
Если PowerShell ругнётся на политику выполнения, выполни один раз:
```bash
Set-ExecutionPolicy -Scope Process Bypass
```

## 1.4 Поставь нужные пакеты
```bash
pip install django pillow
```

## 1.5 Создай Django-проект
```bash
django-admin startproject config .
```

## 1.6 Создай приложения
```bash
python manage.py startapp main
python manage.py startapp accounts
python manage.py startapp festival
python manage.py startapp api
```

## 1.7 Запусти сервер для проверки
```bash
python manage.py runserver
```

---

# 2. Settings
## 2.1 Применяем стандартные миграции
```bash
python manage.py migrate
```

## 2.2 Открываем `config/settings.py`
Найди `INSTALLED_APPS` и добавь наши приложения:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'main',
    'accounts',
    'festival',
    'api',
]
```

Проверь `LANGUAGE_CODE` и `TIME_ZONE`:
```python
LANGUAGE_CODE = 'ru-ru'
TIME_ZONE = 'Asia/Yekaterinburg'
```

Ниже блока `STATIC_URL` добавь это:
```python
STATIC_URL = 'static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'

LOGIN_REDIRECT_URL = 'profile'
LOGOUT_REDIRECT_URL = 'home'
```

## 2.3 Создай папки
```bash
mkdir templates
mkdir static
mkdir media
```

## 2.4 Подключаем общую папку шаблонов
В `config/settings.py` найди блок `TEMPLATES`.

Было:
```python
'DIRS': [],
```

Сделай так:
```python
'DIRS': [BASE_DIR / 'templates'],
```

---

# 3. Главные URL
## 3.1 `config/urls.py`
Полностью замени содержимое:

```python
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
    path('accounts/', include('accounts.urls')),
    path('festival/', include('festival.urls')),
    path('api/', include('api.urls')),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## 3.2 Создай `urls.py` в каждом приложении

### `main/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### `accounts/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.register_view, name='register'),
    path('login/', views.login_view, name='login'),
    path('logout/', views.logout_view, name='logout'),
    path('profile/', views.profile_view, name='profile'),
]
```

### `festival/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('competencies/', views.competencies_view, name='competencies'),
    path('participants/', views.participants_view, name='participants'),
    path('contacts/', views.contacts_view, name='contacts'),
    path('forum/', views.forum_view, name='forum'),
    path('reviews/', views.reviews_view, name='reviews'),
]
```

### `api/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('ping/', views.ping_view, name='api_ping'),
]
```

---

# 4. Временные views, чтобы проект не падал
## `main/views.py`
```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Главная страница")
```

## `accounts/views.py`
```python
from django.http import HttpResponse

def register_view(request):
    return HttpResponse("Регистрация")

def login_view(request):
    return HttpResponse("Авторизация")

def logout_view(request):
    return HttpResponse("Выход")

def profile_view(request):
    return HttpResponse("Личный кабинет")
```

## `festival/views.py`
```python
from django.http import HttpResponse

def competencies_view(request):
    return HttpResponse("Компетенции")

def participants_view(request):
    return HttpResponse("Участники")

def contacts_view(request):
    return HttpResponse("Контакты")

def forum_view(request):
    return HttpResponse("Форум")

def reviews_view(request):
    return HttpResponse("Отзывы")
```

## `api/views.py`
```python
from django.http import JsonResponse

def ping_view(request):
    return JsonResponse({"status": "ok"})
```

## Запусти сервер снова
```bash
python manage.py runserver
```
Проверь:
```text
http://127.0.0.1:8000/
http://127.0.0.1:8000/accounts/register/
http://127.0.0.1:8000/festival/competencies/
http://127.0.0.1:8000/api/ping/
```

---

# 5. Модели
## `accounts/models.py`
```python
from django.db import models
from django.contrib.auth.models import User


class Region(models.Model):
    name = models.CharField(max_length=100, verbose_name='Название региона')

    def __str__(self):
        return self.name

    class Meta:
        verbose_name = 'Регион'
        verbose_name_plural = 'Регионы'


class ParticipantProfile(models.Model):
    CATEGORY_CHOICES = [
        ('student', 'Студент'),
        ('specialist', 'Специалист'),
        ('expert', 'Эксперт'),
    ]

    user = models.OneToOneField(User, on_delete=models.CASCADE, verbose_name='Пользователь')
    middle_name = models.CharField(max_length=100, blank=True, verbose_name='Отчество')
    education = models.CharField(max_length=200, blank=True, verbose_name='Образование')
    institution = models.CharField(max_length=255, blank=True, verbose_name='Учебное заведение')
    region = models.ForeignKey(Region, on_delete=models.SET_NULL, null=True, blank=True, verbose_name='Регион')
    photo = models.ImageField(upload_to='profiles/', blank=True, null=True, verbose_name='Фото')
    category = models.CharField(max_length=20, choices=CATEGORY_CHOICES, default='student', verbose_name='Категория')

    def __str__(self):
        return f'{self.user.last_name} {self.user.first_name}'

    class Meta:
        verbose_name = 'Профиль участника'
        verbose_name_plural = 'Профили участников'
```

## `festival/models.py`
```python
from django.db import models
from django.contrib.auth.models import User
from accounts.models import ParticipantProfile


class Competency(models.Model):
    title = models.CharField(max_length=200, verbose_name='Название компетенции')
    description = models.TextField(verbose_name='Описание')
    task_file = models.FileField(upload_to='tasks/', blank=True, null=True, verbose_name='Файл задания')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'Компетенция'
        verbose_name_plural = 'Компетенции'


class Event(models.Model):
    title = models.CharField(max_length=200, verbose_name='Название мероприятия')
    description = models.TextField(verbose_name='Описание')
    date = models.DateField(verbose_name='Дата')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'Мероприятие'
        verbose_name_plural = 'Мероприятия'


class Application(models.Model):
    STATUS_CHOICES = [
        ('new', 'Новая'),
        ('approved', 'Одобрена'),
        ('rejected', 'Отклонена'),
    ]

    profile = models.ForeignKey(ParticipantProfile, on_delete=models.CASCADE, verbose_name='Профиль')
    competency = models.ForeignKey(Competency, on_delete=models.CASCADE, verbose_name='Компетенция')
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='new', verbose_name='Статус')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Дата создания')

    def __str__(self):
        return f'{self.profile} - {self.competency}'

    class Meta:
        verbose_name = 'Заявка'
        verbose_name_plural = 'Заявки'


class Review(models.Model):
    profile = models.ForeignKey(ParticipantProfile, on_delete=models.CASCADE, verbose_name='Профиль')
    competency = models.ForeignKey(Competency, on_delete=models.CASCADE, verbose_name='Компетенция')
    rating = models.PositiveSmallIntegerField(verbose_name='Оценка')
    comment = models.TextField(verbose_name='Комментарий')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Дата создания')

    def __str__(self):
        return f'Отзыв: {self.profile}'

    class Meta:
        verbose_name = 'Отзыв'
        verbose_name_plural = 'Отзывы'


class ForumPost(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE, verbose_name='Пользователь')
    title = models.CharField(max_length=200, verbose_name='Заголовок')
    message = models.TextField(verbose_name='Сообщение')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Дата создания')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'Сообщение форума'
        verbose_name_plural = 'Сообщения форума'
```

## Миграции
```bash
python manage.py makemigrations accounts
python manage.py makemigrations festival
python manage.py migrate
```

---

# 6. Админка
## `accounts/admin.py`
```python
from django.contrib import admin
from .models import Region, ParticipantProfile


@admin.register(Region)
class RegionAdmin(admin.ModelAdmin):
    list_display = ('id', 'name')
    search_fields = ('name',)


@admin.register(ParticipantProfile)
class ParticipantProfileAdmin(admin.ModelAdmin):
    list_display = ('id', 'user', 'category', 'region')
    list_filter = ('category', 'region')
    search_fields = ('user__first_name', 'user__last_name', 'user__username')
```

## `festival/admin.py`
```python
from django.contrib import admin
from .models import Competency, Event, Application, Review, ForumPost


@admin.register(Competency)
class CompetencyAdmin(admin.ModelAdmin):
    list_display = ('id', 'title')
    search_fields = ('title',)


@admin.register(Event)
class EventAdmin(admin.ModelAdmin):
    list_display = ('id', 'title', 'date')
    search_fields = ('title',)
    list_filter = ('date',)


@admin.register(Application)
class ApplicationAdmin(admin.ModelAdmin):
    list_display = ('id', 'profile', 'competency', 'status', 'created_at')
    list_filter = ('status', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(Review)
class ReviewAdmin(admin.ModelAdmin):
    list_display = ('id', 'profile', 'competency', 'rating', 'created_at')
    list_filter = ('rating', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(ForumPost)
class ForumPostAdmin(admin.ModelAdmin):
    list_display = ('id', 'title', 'user', 'created_at')
    search_fields = ('title', 'user__username')
```

## Создаём администратора
```bash
python manage.py createsuperuser
```

## Запускаем проект
```bash
python manage.py runserver
```

Открывай:
```text
http://127.0.0.1:8000/admin/
```

## Что дальше руками добавить в админке
**Регионы**
- Челябинская область
- Свердловская область
- Тюменская область

**Компетенции**
- Веб-разработка
- Графический дизайн
- Обработка текста
- Программирование
- Сетевое и системное администрирование

**Мероприятия**
- Открытие фестиваля
- Соревнования по компетенциям
- Церемония награждения

---

# 7. Шаблоны и Bootstrap
## 7.1 Создай папки шаблонов
```text
templates/
main/templates/main/
accounts/templates/accounts/
festival/templates/festival/
```

## 7.2 `templates/base.html`
```html
{% load static %}
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Фестиваль возможностей{% endblock %}</title>
    <meta name="description" content="{% block description %}Веб-приложение фестиваля возможностей{% endblock %}">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>

<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container">
        <a class="navbar-brand fw-bold" href="{% url 'home' %}">Фестиваль возможностей</a>

        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarMain">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarMain">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                <li class="nav-item"><a class="nav-link" href="{% url 'home' %}">Главная</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'competencies' %}">Компетенции</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'participants' %}">Участники</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'contacts' %}">Контакты</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'forum' %}">Форум</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'reviews' %}">Отзывы</a></li>

                {% if user.is_authenticated %}
                    <li class="nav-item"><a class="nav-link" href="{% url 'profile' %}">Личный кабинет</a></li>
                    <li class="nav-item"><a class="nav-link" href="{% url 'logout' %}">Выход</a></li>
                {% else %}
                    <li class="nav-item"><a class="nav-link" href="{% url 'register' %}">Регистрация</a></li>
                    <li class="nav-item"><a class="nav-link" href="{% url 'login' %}">Вход</a></li>
                {% endif %}
            </ul>
        </div>
    </div>
</nav>

<main class="py-4">
    <div class="container">
        {% block content %}{% endblock %}
    </div>
</main>

<footer class="bg-light border-top py-4 mt-5">
    <div class="container">
        <div class="row">
            <div class="col-md-6">
                <h5>Фестиваль возможностей</h5>
                <p class="mb-1">Поддержка инклюзивного образования и профессионального роста.</p>
            </div>
            <div class="col-md-6 text-md-end">
                <p class="mb-1">Телефон: +7 (900) 000-00-00</p>
                <p class="mb-1">Email: info@festival.ru</p>
                <p class="mb-0">VK · Telegram · RuTube</p>
            </div>
        </div>
    </div>
</footer>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## 7.3 `static/css/style.css`
```css
body {
    background-color: #f8f9fa;
}

.hero-box {
    background: linear-gradient(135deg, #0d6efd, #6ea8fe);
    color: white;
    padding: 60px 30px;
    border-radius: 20px;
}

.card {
    border-radius: 16px;
}

.section-title {
    margin-bottom: 24px;
    font-weight: 700;
}
```

---

# 8. Views через render
## `main/views.py`
```python
from django.shortcuts import render

def home(request):
    return render(request, 'main/home.html')
```

## `accounts/views.py`
```python
from django.shortcuts import render

def register_view(request):
    return render(request, 'accounts/register.html')

def login_view(request):
    return render(request, 'accounts/login.html')

def logout_view(request):
    return render(request, 'accounts/logout.html')

def profile_view(request):
    return render(request, 'accounts/profile.html')
```

## `festival/views.py`
```python
from django.shortcuts import render
from .models import Competency, Review, ForumPost
from accounts.models import ParticipantProfile


def competencies_view(request):
    competencies = Competency.objects.all()
    return render(request, 'festival/competencies.html', {
        'competencies': competencies
    })


def participants_view(request):
    participants = ParticipantProfile.objects.select_related('user', 'region').all()
    return render(request, 'festival/participants.html', {
        'participants': participants
    })


def contacts_view(request):
    return render(request, 'festival/contacts.html')


def forum_view(request):
    posts = ForumPost.objects.select_related('user').order_by('-created_at')
    return render(request, 'festival/forum.html', {
        'posts': posts
    })


def reviews_view(request):
    reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')
    return render(request, 'festival/reviews.html', {
        'reviews': reviews
    })
```

---

# 9. HTML страницы
## `main/templates/main/home.html`
```html
{% extends 'base.html' %}

{% block title %}Главная | Фестиваль возможностей{% endblock %}
{% block description %}Главная страница фестиваля возможностей{% endblock %}

{% block content %}
<div class="hero-box mb-5">
    <h1 class="display-5 fw-bold">Фестиваль возможностей</h1>
    <p class="lead">Площадка для развития, общения, профессионального роста и демонстрации талантов участников.</p>
    <a href="{% url 'competencies' %}" class="btn btn-light btn-lg mt-3">Смотреть компетенции</a>
</div>

<div class="row g-4">
    <div class="col-md-4">
        <div class="card h-100 shadow-sm"><div class="card-body"><h3 class="h5">О фестивале</h3><p>Фестиваль объединяет участников, экспертов и организаторов.</p></div></div>
    </div>
    <div class="col-md-4">
        <div class="card h-100 shadow-sm"><div class="card-body"><h3 class="h5">Мероприятия</h3><p>В программе фестиваля: презентации, конкурсные задания и мастер-классы.</p></div></div>
    </div>
    <div class="col-md-4">
        <div class="card h-100 shadow-sm"><div class="card-body"><h3 class="h5">Участники</h3><p>На сайте будут представлены участники, компетенции, отзывы и регистрация.</p></div></div>
    </div>
</div>
{% endblock %}
```

## `accounts/templates/accounts/register.html`
```html
{% extends 'base.html' %}
{% block title %}Регистрация{% endblock %}
{% block content %}
<h1 class="section-title">Регистрация</h1>
<div class="card shadow-sm"><div class="card-body"><p>Здесь будет форма регистрации участника.</p></div></div>
{% endblock %}
```

## `accounts/templates/accounts/login.html`
```html
{% extends 'base.html' %}
{% block title %}Вход{% endblock %}
{% block content %}
<h1 class="section-title">Авторизация</h1>
<div class="card shadow-sm"><div class="card-body"><p>Здесь будет форма входа.</p></div></div>
{% endblock %}
```

## `accounts/templates/accounts/logout.html`
```html
{% extends 'base.html' %}
{% block title %}Выход{% endblock %}
{% block content %}
<h1 class="section-title">Выход</h1>
<div class="alert alert-info">Здесь позже сделаем выход из аккаунта.</div>
{% endblock %}
```

## `accounts/templates/accounts/profile.html`
```html
{% extends 'base.html' %}
{% block title %}Личный кабинет{% endblock %}
{% block content %}
<h1 class="section-title">Личный кабинет</h1>
<div class="card shadow-sm"><div class="card-body"><p>Здесь будет профиль пользователя, заявки и отзывы.</p></div></div>
{% endblock %}
```

## `festival/templates/festival/competencies.html`
```html
{% extends 'base.html' %}
{% block title %}Компетенции{% endblock %}
{% block content %}
<h1 class="section-title">Компетенции</h1>
<div class="row g-4">
    {% for competency in competencies %}
        <div class="col-md-6">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h2 class="h5">{{ competency.title }}</h2>
                    <p>{{ competency.description }}</p>
                    {% if competency.task_file %}
                        <a href="{{ competency.task_file.url }}" class="btn btn-primary btn-sm" download>Скачать задание</a>
                    {% else %}
                        <span class="text-muted">Файл пока не загружен</span>
                    {% endif %}
                </div>
            </div>
        </div>
    {% empty %}
        <p>Компетенции пока не добавлены.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/participants.html`
```html
{% extends 'base.html' %}
{% block title %}Участники{% endblock %}
{% block content %}
<h1 class="section-title">Участники</h1>
<div class="row g-4">
    {% for participant in participants %}
        <div class="col-md-6 col-lg-4">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    {% if participant.photo %}
                        <img src="{{ participant.photo.url }}" alt="Фото участника" class="img-fluid rounded mb-3">
                    {% endif %}
                    <h2 class="h5">{{ participant.user.last_name }} {{ participant.user.first_name }} {{ participant.middle_name }}</h2>
                    <p class="mb-1"><strong>Категория:</strong> {{ participant.get_category_display }}</p>
                    <p class="mb-1"><strong>Регион:</strong> {{ participant.region }}</p>
                    <p class="mb-1"><strong>Образование:</strong> {{ participant.education }}</p>
                    <p class="mb-0"><strong>Учреждение:</strong> {{ participant.institution }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Участники пока не добавлены.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/contacts.html`
```html
{% extends 'base.html' %}
{% block title %}Контакты{% endblock %}
{% block content %}
<h1 class="section-title">Контакты</h1>
<div class="card shadow-sm"><div class="card-body"><p><strong>Телефон:</strong> +7 (900) 000-00-00</p><p><strong>Email:</strong> info@festival.ru</p><p><strong>Соцсети:</strong> VK, Telegram, RuTube</p></div></div>
{% endblock %}
```

## `festival/templates/festival/forum.html`
```html
{% extends 'base.html' %}
{% block title %}Форум{% endblock %}
{% block content %}
<h1 class="section-title">Форум</h1>
<div class="row g-4">
    {% for post in posts %}
        <div class="col-12">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h2 class="h5">{{ post.title }}</h2>
                    <p>{{ post.message }}</p>
                    <p class="mb-1"><strong>Автор:</strong> {{ post.user.username }}</p>
                    <small class="text-muted">{{ post.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>На форуме пока нет сообщений.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/reviews.html`
```html
{% extends 'base.html' %}
{% block title %}Отзывы{% endblock %}
{% block content %}
<h1 class="section-title">Отзывы</h1>
<div class="row g-4">
    {% for review in reviews %}
        <div class="col-md-6">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h2 class="h5">{{ review.profile.user.last_name }} {{ review.profile.user.first_name }}</h2>
                    <p class="mb-1"><strong>Компетенция:</strong> {{ review.competency.title }}</p>
                    <p class="mb-1"><strong>Оценка:</strong> {{ review.rating }}/5</p>
                    <p>{{ review.comment }}</p>
                    <small class="text-muted">{{ review.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Отзывов пока нет.</p>
    {% endfor %}
</div>
{% endblock %}
```

---

# 10. Следующий блок: формы

# 10.1 Forms
## `accounts/forms.py`
```python
from django import forms
from django.contrib.auth.models import User
from .models import ParticipantProfile


class RegisterUserForm(forms.ModelForm):
    password = forms.CharField(widget=forms.PasswordInput, label='Пароль')
    password2 = forms.CharField(widget=forms.PasswordInput, label='Подтверждение пароля')
    middle_name = forms.CharField(required=False, label='Отчество')
    education = forms.CharField(required=False, label='Образование')
    institution = forms.CharField(required=False, label='Учебное заведение')
    category = forms.ChoiceField(choices=ParticipantProfile.CATEGORY_CHOICES, label='Категория')
    photo = forms.ImageField(required=False, label='Фото')

    class Meta:
        model = User
        fields = ['username', 'first_name', 'last_name', 'email']
        labels = {
            'username': 'Логин',
            'first_name': 'Имя',
            'last_name': 'Фамилия',
            'email': 'Email',
        }

    def clean(self):
        cleaned_data = super().clean()
        password = cleaned_data.get('password')
        password2 = cleaned_data.get('password2')

        if password and len(password) < 8:
            self.add_error('password', 'Пароль должен быть не менее 8 символов')

        if password and password2 and password != password2:
            self.add_error('password2', 'Пароли не совпадают')

        return cleaned_data
```

## `festival/forms.py`
```python
from django import forms
from .models import Application, Review, ForumPost


class ApplicationForm(forms.ModelForm):
    class Meta:
        model = Application
        fields = ['competency']
        labels = {
            'competency': 'Выберите компетенцию',
        }


class ReviewForm(forms.ModelForm):
    class Meta:
        model = Review
        fields = ['competency', 'rating', 'comment']
        labels = {
            'competency': 'Компетенция',
            'rating': 'Оценка',
            'comment': 'Комментарий',
        }


class ForumPostForm(forms.ModelForm):
    class Meta:
        model = ForumPost
        fields = ['title', 'message']
        labels = {
            'title': 'Заголовок',
            'message': 'Сообщение',
        }
```

---

# 10.2 Регистрация
## `accounts/views.py`
Замени на это:
```python
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout, authenticate
from django.contrib.auth.forms import AuthenticationForm
from .forms import RegisterUserForm
from .models import ParticipantProfile


def register_view(request):
    if request.method == 'POST':
        form = RegisterUserForm(request.POST, request.FILES)
        if form.is_valid():
            user = form.save(commit=False)
            user.set_password(form.cleaned_data['password'])
            user.save()

            ParticipantProfile.objects.create(
                user=user,
                middle_name=form.cleaned_data.get('middle_name', ''),
                education=form.cleaned_data.get('education', ''),
                institution=form.cleaned_data.get('institution', ''),
                category=form.cleaned_data.get('category', 'student'),
                photo=form.cleaned_data.get('photo'),
            )

            login(request, user)
            return redirect('profile')
    else:
        form = RegisterUserForm()

    return render(request, 'accounts/register.html', {'form': form})


def login_view(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            user = form.get_user()
            login(request, user)
            return redirect('profile')
    else:
        form = AuthenticationForm()

    return render(request, 'accounts/login.html', {'form': form})


def logout_view(request):
    logout(request)
    return redirect('home')


def profile_view(request):
    return render(request, 'accounts/profile.html')
```

## `accounts/templates/accounts/register.html`
```html
{% extends 'base.html' %}
{% block title %}Регистрация{% endblock %}
{% block content %}
<h1 class="section-title">Регистрация</h1>
<div class="card shadow-sm">
    <div class="card-body">
        <form method="post" enctype="multipart/form-data">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
        </form>
    </div>
</div>
{% endblock %}
```

---

# 10.3 Логин / Logout
## `accounts/templates/accounts/login.html`
```html
{% extends 'base.html' %}
{% block title %}Вход{% endblock %}
{% block content %}
<h1 class="section-title">Авторизация</h1>
<div class="card shadow-sm">
    <div class="card-body">
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-success">Войти</button>
        </form>
    </div>
</div>
{% endblock %}
```

`logout_view` уже сделан во views.

---

# 10.4 Заявка на участие
## Обнови `accounts/views.py`
```python
from django.contrib.auth.decorators import login_required
from festival.forms import ApplicationForm, ReviewForm
from festival.models import Application


@login_required
def profile_view(request):
    profile = request.user.participantprofile

    if request.method == 'POST':
        app_form = ApplicationForm(request.POST)
        review_form = ReviewForm()

        if app_form.is_valid():
            application = app_form.save(commit=False)
            application.profile = profile
            application.save()
            return redirect('profile')
    else:
        app_form = ApplicationForm()
        review_form = ReviewForm()

    applications = Application.objects.filter(profile=profile).select_related('competency')

    return render(request, 'accounts/profile.html', {
        'app_form': app_form,
        'review_form': review_form,
        'applications': applications,
    })
```

## `accounts/templates/accounts/profile.html`
```html
{% extends 'base.html' %}
{% block title %}Личный кабинет{% endblock %}
{% block content %}
<h1 class="section-title">Личный кабинет</h1>

<div class="row g-4">
    <div class="col-md-6">
        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">Подать заявку</h2>
                <form method="post">
                    {% csrf_token %}
                    {{ app_form.as_p }}
                    <button type="submit" class="btn btn-primary">Отправить заявку</button>
                </form>
            </div>
        </div>
    </div>

    <div class="col-md-6">
        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">Мои заявки</h2>
                {% for application in applications %}
                    <p>
                        <strong>{{ application.competency.title }}</strong><br>
                        Статус: {{ application.get_status_display }}
                    </p>
                {% empty %}
                    <p>Заявок пока нет.</p>
                {% endfor %}
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

---

# 10.5 Отзыв
## Доработай `accounts/views.py`
```python
@login_required
def profile_view(request):
    profile = request.user.participantprofile

    if request.method == 'POST' and 'send_application' in request.POST:
        app_form = ApplicationForm(request.POST)
        review_form = ReviewForm()

        if app_form.is_valid():
            application = app_form.save(commit=False)
            application.profile = profile
            application.save()
            return redirect('profile')

    elif request.method == 'POST' and 'send_review' in request.POST:
        app_form = ApplicationForm()
        review_form = ReviewForm(request.POST)

        if review_form.is_valid():
            review = review_form.save(commit=False)
            review.profile = profile
            review.save()
            return redirect('profile')
    else:
        app_form = ApplicationForm()
        review_form = ReviewForm()

    applications = Application.objects.filter(profile=profile).select_related('competency')

    return render(request, 'accounts/profile.html', {
        'app_form': app_form,
        'review_form': review_form,
        'applications': applications,
    })
```

## Обнови `accounts/templates/accounts/profile.html`
```html
{% extends 'base.html' %}
{% block title %}Личный кабинет{% endblock %}
{% block content %}
<h1 class="section-title">Личный кабинет</h1>

<div class="row g-4">
    <div class="col-md-6">
        <div class="card shadow-sm mb-4">
            <div class="card-body">
                <h2 class="h5">Подать заявку</h2>
                <form method="post">
                    {% csrf_token %}
                    {{ app_form.as_p }}
                    <button type="submit" name="send_application" class="btn btn-primary">Отправить заявку</button>
                </form>
            </div>
        </div>

        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">Оставить отзыв</h2>
                <form method="post">
                    {% csrf_token %}
                    {{ review_form.as_p }}
                    <button type="submit" name="send_review" class="btn btn-success">Отправить отзыв</button>
                </form>
            </div>
        </div>
    </div>

    <div class="col-md-6">
        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">Мои заявки</h2>
                {% for application in applications %}
                    <p>
                        <strong>{{ application.competency.title }}</strong><br>
                        Статус: {{ application.get_status_display }}
                    </p>
                {% empty %}
                    <p>Заявок пока нет.</p>
                {% endfor %}
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

---

# 10.6 Сообщение на форум
## Обнови `festival/views.py`
```python
from .forms import ForumPostForm


def forum_view(request):
    if request.method == 'POST' and request.user.is_authenticated:
        form = ForumPostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.user = request.user
            post.save()
            return redirect('forum')
    else:
        form = ForumPostForm()

    posts = ForumPost.objects.select_related('user').order_by('-created_at')
    return render(request, 'festival/forum.html', {
        'posts': posts,
        'form': form,
    })
```

## Обнови `festival/templates/festival/forum.html`
```html
{% extends 'base.html' %}
{% block title %}Форум{% endblock %}
{% block content %}
<h1 class="section-title">Форум</h1>

{% if user.is_authenticated %}
<div class="card shadow-sm mb-4">
    <div class="card-body">
        <h2 class="h5">Новое сообщение</h2>
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Опубликовать</button>
        </form>
    </div>
</div>
{% endif %}

<div class="row g-4">
    {% for post in posts %}
        <div class="col-12">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h2 class="h5">{{ post.title }}</h2>
                    <p>{{ post.message }}</p>
                    <p class="mb-1"><strong>Автор:</strong> {{ post.user.username }}</p>
                    <small class="text-muted">{{ post.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>На форуме пока нет сообщений.</p>
    {% endfor %}
</div>
{% endblock %}
```
