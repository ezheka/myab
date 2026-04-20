# Подготовка
```
python --version
pip --version
git --version
```

# Поднятие проекта
1. Создай папку проекта
```
cd C:\Users\efimz\Desktop
mkdir abilympics_festival
cd abilympics_festival
```

2. Создай виртуальное окружение
```
python -m venv venv
```

3. Активируй его
```
.\venv\Scripts\Activate.ps1
```
Если PowerShell ругнётся на политику выполнения, выполни один раз:
```
Set-ExecutionPolicy -Scope Process Bypass
```

5. Поставь нужные пакеты
```
pip install django pillow
```

6. Создай Django-проект
```
django-admin startproject config .
```

7. Создай приложения
```
python manage.py startapp main
python manage.py startapp accounts
python manage.py startapp festival
python manage.py startapp api
```

8. Запусти сервер для проверки
```
python manage.py runserver
```

# Settings
1. Применяем стандартные миграции
```
python manage.py migrate
```

2. Открываем config/settings.py
Нужно внести несколько изменений.  
Найди INSTALLED_APPS и добавь наши приложения  
Должно стать так:
```
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
Проверь LANGUAGE_CODE и TIME_ZONE  
Поставь так:
```
LANGUAGE_CODE = 'ru-ru'
TIME_ZONE = 'Asia/Yekaterinburg'
```

Ниже блока STATIC_URL добавь это
```
STATIC_URL = 'static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'

LOGIN_REDIRECT_URL = 'profile'
LOGOUT_REDIRECT_URL = 'home'
```

3. Создай папки
В корне проекта создай папки:
```
mkdir templates
mkdir static
mkdir media
```

4. Подключаем общую папку шаблонов
В config/settings.py найди блок TEMPLATES.  
Там будет строка:  
'DIRS': [],  
Замени на:
```
'DIRS': [BASE_DIR / 'templates'],
```

5. Настраиваем главный urls.py
Открой файл config/urls.py и полностью замени содержимое на это:
```
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

6. Создай urls.py в каждом приложении
main/urls.py
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

accounts/urls.py
```
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.register_view, name='register'),
    path('login/', views.login_view, name='login'),
    path('logout/', views.logout_view, name='logout'),
    path('profile/', views.profile_view, name='profile'),
]
```

festival/urls.py
```
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

api/urls.py
```
from django.urls import path
from . import views

urlpatterns = [
    path('ping/', views.ping_view, name='api_ping'),
]
```

7. Делаем временные views, чтобы проект не падал
main/views.py
```
from django.http import HttpResponse

def home(request):
    return HttpResponse("Главная страница")
```
accounts/views.py
```
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
festival/views.py
```
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

api/views.py
```
from django.http import JsonResponse

def ping_view(request):
    return JsonResponse({"status": "ok"})
```

8. Запусти сервер снова
```
python manage.py runserver
```
И проверь в браузере:
```
http://127.0.0.1:8000/
http://127.0.0.1:8000/accounts/register/
http://127.0.0.1:8000/festival/competencies/
http://127.0.0.1:8000/api/ping/
```

# Модели
accounts/models.py
```
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

festival/models.py
```
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

2. Делаем миграции
В терминале по очереди:
```
python manage.py makemigrations accounts
python manage.py makemigrations festival
python manage.py migrate
```

3. Подключаем модели в админку
accounts/admin.py
```
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

festival/admin.py
```
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

4. Создаём администратора
```
python manage.py createsuperuser
```

5. Запускаем проект
```
python manage.py runserver
```

Открывай:
```
http://127.0.0.1:8000/admin/
```

6. Что дальше руками добавить в админке
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
