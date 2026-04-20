# README — цельный шаблон проекта без промежуточных обновлений

Этот вариант нужен для заучивания.  
Здесь логика такая:

- создаёшь проект;
- сразу создаёшь нужные файлы;
- сразу вставляешь в них финальный код;
- потом делаешь миграции, админку и запуск.

---

# 1. Подготовка

Проверка:

```bash
python --version
pip --version
git --version
```

Создание проекта:

```bash
cd C:\Users\efimz\Desktop
mkdir abilympics_festival
cd abilympics_festival

python -m venv venv
.\venv\Scripts\Activate.ps1
pip install django pillow

django-admin startproject config .
python manage.py startapp main
python manage.py startapp accounts
python manage.py startapp festival
python manage.py startapp api
```

Создай папки:

```bash
mkdir templates
mkdir static
mkdir media
mkdir static\css
mkdir main\templates\main
mkdir accounts\templates\accounts
mkdir festival\templates\festival
```

---

# 2. Сразу вставляй готовый `config/settings.py`

Открой `config/settings.py` и проверь/замени нужные части.

## INSTALLED_APPS

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

## Язык и время

```python
LANGUAGE_CODE = 'ru-ru'
TIME_ZONE = 'Asia/Yekaterinburg'
USE_I18N = True
USE_TZ = True
```

## Шаблоны

Найди в `TEMPLATES` строку:

```python
'DIRS': [],
```

Замени на:

```python
'DIRS': [BASE_DIR / 'templates'],
```

## Статика и медиа

Ниже добавь:

```python
STATIC_URL = 'static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'

LOGIN_REDIRECT_URL = 'profile'
LOGOUT_REDIRECT_URL = 'home'
```

---

# 3. Сразу вставляй готовый `config/urls.py`

Файл `config/urls.py`:

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

---

# 4. Сразу создавай все `urls.py`

## `main/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

## `accounts/urls.py`

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

## `festival/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('competencies/', views.competencies_view, name='competencies'),
    path('participants/', views.participants_view, name='participants'),
    path('contacts/', views.contacts_view, name='contacts'),
    path('forum/', views.forum_view, name='forum'),
    path('reviews/', views.reviews_view, name='reviews'),
    path('apply/', views.apply_view, name='apply'),
    path('review/create/', views.create_review_view, name='create_review'),
    path('forum/create/', views.create_forum_post_view, name='create_forum_post'),
]
```

## `api/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('ping/', views.ping_view, name='api_ping'),
]
```

---

# 5. Сразу создавай модели

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

---

# 6. Сразу создавай формы

## `accounts/forms.py`

```python
from django import forms
from .models import Region


class RegisterUserForm(forms.Form):
    username = forms.CharField(label='Логин', max_length=150)
    first_name = forms.CharField(label='Имя', max_length=150)
    last_name = forms.CharField(label='Фамилия', max_length=150)
    middle_name = forms.CharField(label='Отчество', max_length=150, required=False)
    email = forms.EmailField(label='Email')
    password1 = forms.CharField(label='Пароль', widget=forms.PasswordInput)
    password2 = forms.CharField(label='Подтверждение пароля', widget=forms.PasswordInput)
    education = forms.CharField(label='Образование', max_length=200, required=False)
    institution = forms.CharField(label='Учебное заведение', max_length=255, required=False)
    region = forms.ModelChoiceField(label='Регион', queryset=Region.objects.all(), required=False)
    photo = forms.ImageField(label='Фото', required=False)
    category = forms.ChoiceField(
        label='Категория',
        choices=[
            ('student', 'Студент'),
            ('specialist', 'Специалист'),
            ('expert', 'Эксперт'),
        ]
    )

    def clean(self):
        cleaned_data = super().clean()
        password1 = cleaned_data.get('password1')
        password2 = cleaned_data.get('password2')

        if password1 and password2 and password1 != password2:
            raise forms.ValidationError('Пароли не совпадают')

        if password1 and len(password1) < 8:
            raise forms.ValidationError('Пароль должен быть не менее 8 символов')

        return cleaned_data
```

## `festival/forms.py`

```python
from django import forms
from .models import Application, Review, ForumPost, Competency


class ApplicationForm(forms.ModelForm):
    class Meta:
        model = Application
        fields = ['competency']


class ReviewForm(forms.ModelForm):
    class Meta:
        model = Review
        fields = ['competency', 'rating', 'comment']


class ForumPostForm(forms.ModelForm):
    class Meta:
        model = ForumPost
        fields = ['title', 'message']
```

---

# 7. Сразу создавай views

## `main/views.py`

```python
from django.shortcuts import render
from festival.models import Event, Review


def home(request):
    events = Event.objects.order_by('date')[:3]
    latest_reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')[:4]
    return render(request, 'main/home.html', {
        'events': events,
        'latest_reviews': latest_reviews,
    })
```

## `accounts/views.py`

```python
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout, authenticate
from django.contrib.auth.decorators import login_required
from django.contrib.auth.models import User

from .forms import RegisterUserForm
from .models import ParticipantProfile


def register_view(request):
    if request.method == 'POST':
        form = RegisterUserForm(request.POST, request.FILES)
        if form.is_valid():
            user = User.objects.create_user(
                username=form.cleaned_data['username'],
                first_name=form.cleaned_data['first_name'],
                last_name=form.cleaned_data['last_name'],
                email=form.cleaned_data['email'],
                password=form.cleaned_data['password1'],
            )

            ParticipantProfile.objects.create(
                user=user,
                middle_name=form.cleaned_data['middle_name'],
                education=form.cleaned_data['education'],
                institution=form.cleaned_data['institution'],
                region=form.cleaned_data['region'],
                photo=form.cleaned_data['photo'],
                category=form.cleaned_data['category'],
            )

            login(request, user)
            return redirect('profile')
    else:
        form = RegisterUserForm()

    return render(request, 'accounts/register.html', {'form': form})


def login_view(request):
    error = ''

    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')

        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('profile')
        else:
            error = 'Неверный логин или пароль'

    return render(request, 'accounts/login.html', {'error': error})


def logout_view(request):
    logout(request)
    return redirect('home')


@login_required
def profile_view(request):
    profile, created = ParticipantProfile.objects.get_or_create(
        user=request.user,
        defaults={
            'middle_name': '',
            'education': '',
            'institution': '',
            'category': 'specialist',
        }
    )

    applications = profile.application_set.select_related('competency').all()
    reviews = profile.review_set.select_related('competency').all()

    return render(request, 'accounts/profile.html', {
        'profile': profile,
        'applications': applications,
        'reviews': reviews,
    })
```

## `festival/views.py`

```python
from django.shortcuts import render, redirect
from django.contrib.auth.decorators import login_required
from .models import Competency, Review, ForumPost
from .forms import ApplicationForm, ReviewForm, ForumPostForm
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
    form = ForumPostForm()
    return render(request, 'festival/forum.html', {
        'posts': posts,
        'form': form,
    })


def reviews_view(request):
    reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')
    form = ReviewForm()
    return render(request, 'festival/reviews.html', {
        'reviews': reviews,
        'form': form,
    })


@login_required
def apply_view(request):
    profile, created = ParticipantProfile.objects.get_or_create(
        user=request.user,
        defaults={'category': 'specialist'}
    )

    if request.method == 'POST':
        form = ApplicationForm(request.POST)
        if form.is_valid():
            application = form.save(commit=False)
            application.profile = profile
            application.save()
            return redirect('profile')
    else:
        form = ApplicationForm()

    return render(request, 'festival/apply.html', {'form': form})


@login_required
def create_review_view(request):
    profile, created = ParticipantProfile.objects.get_or_create(
        user=request.user,
        defaults={'category': 'specialist'}
    )

    if request.method == 'POST':
        form = ReviewForm(request.POST)
        if form.is_valid():
            review = form.save(commit=False)
            review.profile = profile
            review.save()
            return redirect('reviews')

    return redirect('reviews')


@login_required
def create_forum_post_view(request):
    if request.method == 'POST':
        form = ForumPostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.user = request.user
            post.save()
            return redirect('forum')

    return redirect('forum')
```

## `api/views.py`

```python
from django.http import JsonResponse


def ping_view(request):
    return JsonResponse({"status": "ok"})
```

---

# 8. Сразу создавай админку

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

---

# 9. Сразу создавай базовый шаблон

## `templates/base.html`

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
            <ul class="navbar-nav ms-auto">
                <li class="nav-item"><a class="nav-link" href="{% url 'home' %}">Главная</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'competencies' %}">Компетенции</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'participants' %}">Участники</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'contacts' %}">Контакты</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'forum' %}">Форум</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'reviews' %}">Отзывы</a></li>

                {% if user.is_authenticated %}
                    <li class="nav-item"><a class="nav-link" href="{% url 'apply' %}">Заявка</a></li>
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
        <p class="mb-1">Телефон: +7 (900) 000-00-00</p>
        <p class="mb-1">Email: info@festival.ru</p>
        <p class="mb-0">VK · Telegram · RuTube</p>
    </div>
</footer>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

# 10. Сразу создавай CSS

## `static/css/style.css`

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

# 11. Сразу создавай все шаблоны страниц

## `main/templates/main/home.html`

```html
{% extends 'base.html' %}
{% block title %}Главная | Фестиваль возможностей{% endblock %}

{% block content %}
<div class="hero-box mb-5">
    <h1 class="display-5 fw-bold">Фестиваль возможностей</h1>
    <p class="lead">Площадка для развития, общения и профессионального роста.</p>
    <a href="{% url 'competencies' %}" class="btn btn-light btn-lg mt-3">Смотреть компетенции</a>
</div>

<h2 class="section-title">Мероприятия</h2>
<div class="row g-4 mb-5">
    {% for event in events %}
        <div class="col-md-4">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h3 class="h5">{{ event.title }}</h3>
                    <p>{{ event.description }}</p>
                    <p><strong>Дата:</strong> {{ event.date }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Мероприятия пока не добавлены.</p>
    {% endfor %}
</div>

<h2 class="section-title">Последние отзывы</h2>
<div class="row g-4">
    {% for review in latest_reviews %}
        <div class="col-md-6">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h3 class="h5">{{ review.profile.user.last_name }} {{ review.profile.user.first_name }}</h3>
                    <p><strong>Компетенция:</strong> {{ review.competency.title }}</p>
                    <p><strong>Оценка:</strong> {{ review.rating }}/5</p>
                    <p>{{ review.comment }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Отзывов пока нет.</p>
    {% endfor %}
</div>
{% endblock %}
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

## `accounts/templates/accounts/login.html`

```html
{% extends 'base.html' %}
{% block title %}Вход{% endblock %}

{% block content %}
<h1 class="section-title">Авторизация</h1>
<div class="card shadow-sm">
    <div class="card-body">
        {% if error %}
            <div class="alert alert-danger">{{ error }}</div>
        {% endif %}
        <form method="post">
            {% csrf_token %}
            <p>
                <label>Логин</label>
                <input type="text" name="username" class="form-control">
            </p>
            <p>
                <label>Пароль</label>
                <input type="password" name="password" class="form-control">
            </p>
            <button type="submit" class="btn btn-primary">Войти</button>
        </form>
    </div>
</div>
{% endblock %}
```

## `accounts/templates/accounts/profile.html`

```html
{% extends 'base.html' %}
{% block title %}Личный кабинет{% endblock %}

{% block content %}
<h1 class="section-title">Личный кабинет</h1>

<div class="card shadow-sm mb-4">
    <div class="card-body">
        <h2 class="h5">{{ request.user.last_name }} {{ request.user.first_name }}</h2>
        <p><strong>Категория:</strong> {{ profile.get_category_display }}</p>
        <p><strong>Регион:</strong> {{ profile.region }}</p>
        <p><strong>Образование:</strong> {{ profile.education }}</p>
        <p><strong>Учреждение:</strong> {{ profile.institution }}</p>
    </div>
</div>

<h2 class="section-title">Мои заявки</h2>
<div class="row g-4 mb-5">
    {% for application in applications %}
        <div class="col-md-6">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h3 class="h5">{{ application.competency.title }}</h3>
                    <p><strong>Статус:</strong> {{ application.get_status_display }}</p>
                    <p><strong>Дата:</strong> {{ application.created_at }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Заявок пока нет.</p>
    {% endfor %}
</div>

<h2 class="section-title">Мои отзывы</h2>
<div class="row g-4">
    {% for review in reviews %}
        <div class="col-md-6">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h3 class="h5">{{ review.competency.title }}</h3>
                    <p><strong>Оценка:</strong> {{ review.rating }}/5</p>
                    <p>{{ review.comment }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Отзывов пока нет.</p>
    {% endfor %}
</div>
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
                    <details>
                        <summary>Показать описание</summary>
                        <p class="mt-2">{{ competency.description }}</p>
                    </details>

                    {% if competency.task_file %}
                        <a href="{{ competency.task_file.url }}" class="btn btn-primary btn-sm mt-3" download>Скачать задание</a>
                    {% else %}
                        <span class="text-muted d-block mt-3">Файл пока не загружен</span>
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
                    <p><strong>Категория:</strong> {{ participant.get_category_display }}</p>
                    <p><strong>Регион:</strong> {{ participant.region }}</p>
                    <p><strong>Образование:</strong> {{ participant.education }}</p>
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
<div class="card shadow-sm">
    <div class="card-body">
        <p><strong>Телефон:</strong> +7 (900) 000-00-00</p>
        <p><strong>Email:</strong> info@festival.ru</p>
        <p><strong>Соцсети:</strong> VK, Telegram, RuTube</p>
    </div>
</div>
{% endblock %}
```

## `festival/templates/festival/forum.html`

```html
{% extends 'base.html' %}
{% block title %}Форум{% endblock %}

{% block content %}
<h1 class="section-title">Форум</h1>

<div class="card shadow-sm mb-4">
    <div class="card-body">
        <form method="post" action="{% url 'create_forum_post' %}">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Отправить сообщение</button>
        </form>
    </div>
</div>

<div class="row g-4">
    {% for post in posts %}
        <div class="col-12">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h2 class="h5">{{ post.title }}</h2>
                    <p>{{ post.message }}</p>
                    <p><strong>Автор:</strong> {{ post.user.username }}</p>
                    <small class="text-muted">{{ post.created_at }}</small>
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

<div class="card shadow-sm mb-4">
    <div class="card-body">
        <form method="post" action="{% url 'create_review' %}">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Оставить отзыв</button>
        </form>
    </div>
</div>

<div class="row g-4">
    {% for review in reviews %}
        <div class="col-md-6">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h2 class="h5">{{ review.profile.user.last_name }} {{ review.profile.user.first_name }}</h2>
                    <p><strong>Компетенция:</strong> {{ review.competency.title }}</p>
                    <p><strong>Оценка:</strong> {{ review.rating }}/5</p>
                    <p>{{ review.comment }}</p>
                    <small class="text-muted">{{ review.created_at }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>Отзывов пока нет.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/apply.html`

```html
{% extends 'base.html' %}
{% block title %}Заявка на участие{% endblock %}

{% block content %}
<h1 class="section-title">Заявка на участие</h1>

<div class="card shadow-sm">
    <div class="card-body">
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Подать заявку</button>
        </form>
    </div>
</div>
{% endblock %}
```

---

# 12. Миграции и запуск

```bash
python manage.py makemigrations accounts
python manage.py makemigrations festival
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Админ:
- логин: `admin`
- пароль: `passadmin`

---

# 13. Что добавить в админке

## Регионы
- Челябинская область
- Свердловская область
- Тюменская область

## Компетенции
- Веб-разработка
- Графический дизайн
- Обработка текста
- Программирование
- Сетевое и системное администрирование

## Мероприятия
- Открытие фестиваля
- Соревнования по компетенциям
- Церемония награждения

## Пользователи
- admin
- 2–3 обычных пользователя

## Профили
- создай профили для обычных пользователей

## Отзывы
- добавь 2–3 отзыва

## Форум
- добавь 2–3 сообщения

---

# 14. Что проверять в браузере

```text
http://127.0.0.1:8000/
http://127.0.0.1:8000/admin/
http://127.0.0.1:8000/accounts/register/
http://127.0.0.1:8000/accounts/login/
http://127.0.0.1:8000/accounts/profile/
http://127.0.0.1:8000/festival/competencies/
http://127.0.0.1:8000/festival/participants/
http://127.0.0.1:8000/festival/contacts/
http://127.0.0.1:8000/festival/forum/
http://127.0.0.1:8000/festival/reviews/
http://127.0.0.1:8000/festival/apply/
http://127.0.0.1:8000/api/ping/
```

---

# 15. Что запомнить для конкурса

Минимальная логика такая:

1. создать проект и apps  
2. вставить settings  
3. вставить urls  
4. вставить models  
5. вставить forms  
6. вставить views  
7. вставить admin  
8. вставить шаблоны  
9. сделать миграции  
10. создать admin  
11. наполнить админку данными  
12. проверить страницы
