# 0. Команды для терминала

## Запуск без истории

```bash
Set-PSReadLineOption -HistorySaveStyle SaveNothing
Set-PSReadLineOption -AddToHistoryHandler { param($line) $false }
[Microsoft.PowerShell.PSConsoleReadLine]::ClearHistory()

function ghread {
    param([string]$File = 'README.md')
    $wc = New-Object System.Net.WebClient
    $bytes = $wc.DownloadData("https://raw.githubusercontent.com/ezheka/myab/main/$File")
    [System.Text.Encoding]::UTF8.GetString($bytes) -split "\r?\n" | Out-Host -Paging
}
```

## Вывод файла

```bash
ghread README.md
```

## Чистка команды в истории

```bash
(Get-PSReadLineOption).HistorySavePath
```

# 01. Поднятие проекта

## Проверка инструментов

```bash
python --version
pip --version
git --version
```

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

# 02. Settings

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

    # Наши приложения проекта.
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
# Отсюда Django будет брать общие CSS и другие статические файлы проекта.
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = 'media/'
# Сюда будут сохраняться фотографии профилей и файлы заданий.
MEDIA_ROOT = BASE_DIR / 'media'

# После входа пользователя сразу отправляем в личный кабинет.
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
'DIRS': [BASE_DIR / 'templates'],  # Подключаем общую папку с базовым шаблоном.
```

---

# 03. Главные URL

## 3.1 `config/urls.py`

Полностью замени содержимое:

```python
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    # Подключаем админку, главную страницу, аккаунты, раздел фестиваля и API.
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
    path('accounts/', include('accounts.urls')),
    path('festival/', include('festival.urls')),
    path('api/', include('api.urls')),
]

if settings.DEBUG:
    # Во время разработки разрешаем Django отдавать загруженные медиа-файлы.
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## 3.2 Создай `urls.py` в каждом приложении

### `main/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    # Корневой адрес сайта открывает главную страницу.
    path('', views.home, name='home'),
]
```

### `accounts/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    # Маршруты регистрации, входа, выхода и личного кабинета.
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
    # Основные публичные страницы фестиваля.
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
    # Тестовая API-точка для проверки JSON-ответа.
    path('ping/', views.ping_view, name='api_ping'),
]
```

---

# 04. Временные views, чтобы проект не падал

## `main/views.py`

```python
from django.http import HttpResponse

def home(request):
    # Временная заглушка, чтобы сразу проверить маршрут без шаблонов.
    return HttpResponse("Главная страница")
```

## `accounts/views.py`

```python
from django.http import HttpResponse

def register_view(request):
    # Заглушка страницы регистрации до подключения реального шаблона.
    return HttpResponse("Регистрация")

def login_view(request):
    # Заглушка страницы входа.
    return HttpResponse("Авторизация")

def logout_view(request):
    # Заглушка страницы выхода.
    return HttpResponse("Выход")

def profile_view(request):
    # Заглушка личного кабинета.
    return HttpResponse("Личный кабинет")
```

## `festival/views.py`

```python
from django.http import HttpResponse

def competencies_view(request):
    # Временная страница списка компетенций.
    return HttpResponse("Компетенции")

def participants_view(request):
    # Временная страница списка участников.
    return HttpResponse("Участники")

def contacts_view(request):
    # Временная страница контактов.
    return HttpResponse("Контакты")

def forum_view(request):
    # Временная страница форума.
    return HttpResponse("Форум")

def reviews_view(request):
    # Временная страница отзывов.
    return HttpResponse("Отзывы")
```

## `api/views.py`

```python
from django.http import JsonResponse

def ping_view(request):
    # Быстрая проверка, что API отвечает JSON-данными.
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

# 05. Модели

## `accounts/models.py`

```python
from django.db import models
from django.contrib.auth.models import User


class Region(models.Model):
    # Справочник регионов нужен для профиля и фильтрации участников.
    name = models.CharField(max_length=100, verbose_name='Название региона')

    def __str__(self):
        return self.name

    class Meta:
        verbose_name = 'Регион'
        verbose_name_plural = 'Регионы'


class ParticipantProfile(models.Model):
    # Категории пригодятся для вывода на сайте и для фильтров.
    CATEGORY_CHOICES = [
        ('student', 'Студент'),
        ('specialist', 'Специалист'),
        ('expert', 'Эксперт'),
    ]

    # В профиле лежат данные, которых нет в стандартной модели User.
    user = models.OneToOneField(User, on_delete=models.CASCADE, verbose_name='Пользователь')
    middle_name = models.CharField(max_length=100, blank=True, verbose_name='Отчество')
    education = models.CharField(max_length=200, blank=True, verbose_name='Образование')
    institution = models.CharField(max_length=255, blank=True, verbose_name='Учебное заведение')
    region = models.ForeignKey(Region, on_delete=models.SET_NULL, null=True, blank=True, verbose_name='Регион')
    photo = models.ImageField(upload_to='profiles/', blank=True, null=True, verbose_name='Фото')
    category = models.CharField(max_length=20, choices=CATEGORY_CHOICES, default='student', verbose_name='Категория')

    def __str__(self):
        # Так профиль будет красиво отображаться в админке.
        return f'{self.user.last_name} {self.user.first_name}'

    class Meta:
        verbose_name = 'Профиль участника'
        verbose_name_plural = 'Профили участников'
```

## `festival/models.py`

```python
from django.db import models
from django.contrib.auth.models import User
from django.core.validators import MinValueValidator, MaxValueValidator
from accounts.models import ParticipantProfile


class Competency(models.Model):
    # Здесь храним описание компетенции и файл задания для скачивания.
    title = models.CharField(max_length=200, verbose_name='Название компетенции')
    description = models.TextField(verbose_name='Описание')
    task_file = models.FileField(upload_to='tasks/', blank=True, null=True, verbose_name='Файл задания')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'Компетенция'
        verbose_name_plural = 'Компетенции'


class Event(models.Model):
    # Отдельная модель мероприятий нужна для анонсов и расписания.
    title = models.CharField(max_length=200, verbose_name='Название мероприятия')
    description = models.TextField(verbose_name='Описание')
    date = models.DateField(verbose_name='Дата')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'Мероприятие'
        verbose_name_plural = 'Мероприятия'


class Application(models.Model):
    # Статус помогает видеть состояние заявки в кабинете и в админке.
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
        # Удобная подпись для списка заявок.
        return f'{self.profile} - {self.competency}'

    class Meta:
        verbose_name = 'Заявка'
        verbose_name_plural = 'Заявки'


class Review(models.Model):
    # Отзыв хранит оценку и текст комментария участника.
    profile = models.ForeignKey(ParticipantProfile, on_delete=models.CASCADE, verbose_name='Профиль')
    competency = models.ForeignKey(Competency, on_delete=models.CASCADE, verbose_name='Компетенция')
    # Оценку ограничиваем диапазоном от 1 до 5.
    rating = models.PositiveSmallIntegerField(
        verbose_name='Оценка',
        validators=[MinValueValidator(1), MaxValueValidator(5)],
    )
    comment = models.TextField(verbose_name='Комментарий')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Дата создания')

    def __str__(self):
        # В подписи отзыва сохраняем привязку к автору.
        return f'Отзыв: {self.profile}'

    class Meta:
        verbose_name = 'Отзыв'
        verbose_name_plural = 'Отзывы'


class ForumPost(models.Model):
    # Простая модель форума: автор, заголовок, текст и дата создания.
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

# 06. Админка

## `accounts/admin.py`

```python
from django.contrib import admin
from .models import Region, ParticipantProfile


@admin.register(Region)
class RegionAdmin(admin.ModelAdmin):
    # Для регионов достаточно списка и поиска по названию.
    list_display = ('id', 'name')
    search_fields = ('name',)


@admin.register(ParticipantProfile)
class ParticipantProfileAdmin(admin.ModelAdmin):
    # Профили удобно фильтровать по категории и региону.
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
    # Компетенции ищем по названию.
    list_display = ('id', 'title')
    search_fields = ('title',)


@admin.register(Event)
class EventAdmin(admin.ModelAdmin):
    # Для мероприятий отдельно выводим дату и добавляем фильтр по ней.
    list_display = ('id', 'title', 'date')
    search_fields = ('title',)
    list_filter = ('date',)


@admin.register(Application)
class ApplicationAdmin(admin.ModelAdmin):
    # Заявки удобно сортировать и искать по участнику и компетенции.
    list_display = ('id', 'profile', 'competency', 'status', 'created_at')
    list_filter = ('status', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(Review)
class ReviewAdmin(admin.ModelAdmin):
    # У отзывов оставляем фильтр по оценке и компетенции.
    list_display = ('id', 'profile', 'competency', 'rating', 'created_at')
    list_filter = ('rating', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(ForumPost)
class ForumPostAdmin(admin.ModelAdmin):
    # Сообщения форума ищем по заголовку и автору.
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

# 07. Шаблоны и Bootstrap

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

<!-- Общее меню сайта находится в base.html, чтобы не дублировать его на каждой странице. -->
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

<!-- В этот блок Django будет подставлять содержимое дочерних шаблонов. -->
<main class="py-4">
    <div class="container">
        {% block content %}{% endblock %}
    </div>
</main>

<!-- Подвал также общий для всех страниц сайта. -->
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
/* Базовый фон для всех страниц сайта. */
body {
    background-color: #f8f9fa;
}

/* Hero-блок выделяет главную страницу и первый экран. */
.hero-box {
    background: linear-gradient(135deg, #0d6efd, #6ea8fe);
    color: white;
    padding: 60px 30px;
    border-radius: 20px;
}

/* Небольшой бейдж помогает визуально выделить статус фестиваля. */
.hero-badge {
    display: inline-block;
    padding: 8px 14px;
    border-radius: 999px;
    background: rgba(255, 255, 255, 0.18);
    font-size: 0.95rem;
}

/* Карточка обратного отсчёта делает первый экран информативнее. */
.countdown-card {
    background: rgba(255, 255, 255, 0.16);
    border: 1px solid rgba(255, 255, 255, 0.24);
    border-radius: 20px;
    padding: 28px;
    backdrop-filter: blur(6px);
}

/* Подпись внутри счётчика оформляется как вспомогательный текст. */
.countdown-label {
    text-transform: uppercase;
    letter-spacing: 0.08em;
    font-size: 0.8rem;
    opacity: 0.85;
}

/* Крупное число должно сразу бросаться в глаза пользователю. */
.countdown-value {
    font-size: 3rem;
    font-weight: 700;
    line-height: 1;
    margin: 12px 0;
}

/* Слайды в карусели должны выглядеть как большие промо-блоки. */
.promo-slide {
    min-height: 320px;
    padding: 48px 52px;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

/* Заголовок слайда делаем крупным и читабельным. */
.promo-slide h2 {
    max-width: 640px;
    font-size: 2rem;
    margin-bottom: 14px;
}

/* Текст слайда ограничиваем по ширине для удобного чтения. */
.promo-slide p {
    max-width: 580px;
    font-size: 1.05rem;
    margin-bottom: 24px;
}

/* Короткая подпись над заголовком помогает расставить акценты. */
.promo-kicker {
    display: inline-block;
    margin-bottom: 12px;
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    opacity: 0.85;
}

/* Разные цветовые варианты делают слайды визуально живее. */
.promo-slide-blue {
    background: linear-gradient(135deg, #0d6efd, #3d8bfd);
}

.promo-slide-orange {
    background: linear-gradient(135deg, #fd7e14, #ffb357);
}

.promo-slide-green {
    background: linear-gradient(135deg, #198754, #54c78d);
}

/* Полоса статистики слегка наезжает на соседний блок для глубины. */
.stats-strip {
    margin-top: -12px;
}

/* Каждая карточка статистики должна выглядеть как отдельный KPI-блок. */
.stats-card {
    background: white;
    border-radius: 18px;
    padding: 24px;
    box-shadow: 0 0.5rem 1rem rgba(13, 110, 253, 0.08);
    text-align: center;
}

/* Значение статистики делаем крупным и акцентным. */
.stats-value {
    font-size: 2.1rem;
    font-weight: 700;
    color: #0d6efd;
    line-height: 1;
}

/* Подпись под числом нужна для расшифровки показателя. */
.stats-label {
    margin-top: 10px;
    color: #495057;
}

/* Универсальная светлая панель используется в информационных секциях. */
.info-panel {
    background: white;
    border-radius: 20px;
    padding: 28px;
    box-shadow: 0 0.5rem 1rem rgba(33, 37, 41, 0.06);
}

/* Карточки мероприятий выделяются лёгкой синей подложкой. */
.event-card {
    height: 100%;
    background: #f8fbff;
    border: 1px solid #dbe8ff;
    border-radius: 18px;
    padding: 20px;
}

/* Дата мероприятия должна быстро считываться взглядом. */
.event-date {
    color: #0d6efd;
    font-weight: 700;
    margin-bottom: 10px;
}

/* Шаги участия показываем вертикальным списком с номером. */
.step-item {
    display: flex;
    gap: 14px;
    align-items: flex-start;
    margin-bottom: 18px;
}

.step-item:last-child {
    margin-bottom: 0;
}

/* Номер шага оформляем кругом, чтобы порядок читался быстрее. */
.step-number {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: #0d6efd;
    color: white;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    flex-shrink: 0;
}

/* Превью отзывов делаем отдельными карточками для доверия к странице. */
.review-preview-card {
    background: white;
    border-radius: 18px;
    padding: 24px;
    box-shadow: 0 0.5rem 1rem rgba(33, 37, 41, 0.06);
}

/* Оценка отзыва оформляется как заметный бейдж. */
.review-score {
    display: inline-block;
    padding: 8px 12px;
    border-radius: 12px;
    background: #fff3cd;
    color: #856404;
    font-weight: 700;
}

/* Карточки команды делают блок организаторов визуально цельным. */
.team-card {
    background: white;
    border-radius: 18px;
    padding: 24px;
    box-shadow: 0 0.5rem 1rem rgba(33, 37, 41, 0.06);
}

/* Заглушка-аватар помогает оформить карточку даже без фотографии. */
.team-avatar {
    width: 54px;
    height: 54px;
    border-radius: 50%;
    background: linear-gradient(135deg, #0d6efd, #6ea8fe);
    color: white;
    font-size: 1.4rem;
    font-weight: 700;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 16px;
}

/* Роль участника команды подчёркиваем фирменным цветом. */
.team-role {
    color: #0d6efd;
    font-weight: 600;
}

/* Единый радиус делает карточки визуально одинаковыми. */
.card {
    border-radius: 16px;
}

/* Общий стиль заголовков секций. */
.section-title {
    margin-bottom: 24px;
    font-weight: 700;
}

/* На мобильных устройствах уменьшаем отступы и размеры текста. */
@media (max-width: 767.98px) {
    .hero-box {
        padding: 36px 22px;
    }

    .promo-slide {
        min-height: 280px;
        padding: 34px 24px 46px;
    }

    .promo-slide h2 {
        font-size: 1.55rem;
    }

    .countdown-value {
        font-size: 2.4rem;
    }
}
```

---

# 08. Views через render

## `main/views.py`

```python
from django.shortcuts import render
from django.utils import timezone

from accounts.models import ParticipantProfile
from festival.models import Application, Competency, Event, Review

def home(request):
    # Главную страницу собираем из данных проекта, а не держим её статичной.
    today = timezone.localdate()
    next_event = Event.objects.filter(date__gte=today).order_by('date').first()

    if next_event is None:
        # Если будущих мероприятий ещё нет, берём ближайшее доступное из базы.
        next_event = Event.objects.order_by('date').first()

    countdown_days = None
    if next_event:
        countdown_days = max((next_event.date - today).days, 0)

    latest_reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')[:4]
    upcoming_events = Event.objects.order_by('date')[:3]

    stats = {
        'competencies': Competency.objects.count(),
        'participants': ParticipantProfile.objects.count(),
        'applications': Application.objects.count(),
        'reviews': Review.objects.count(),
    }

    team_members = [
        {
            'name': 'Анна Смирнова',
            'role': 'Координатор фестиваля',
            'description': 'Отвечает за расписание, регистрацию и связь с участниками.',
        },
        {
            'name': 'Илья Волков',
            'role': 'Технический эксперт',
            'description': 'Сопровождает конкурсные площадки и проверяет техническую готовность.',
        },
        {
            'name': 'Мария Белова',
            'role': 'Куратор участников',
            'description': 'Помогает с навигацией по сайту, заявками и обратной связью.',
        },
    ]

    return render(request, 'main/home.html', {
        'countdown_days': countdown_days,
        'next_event': next_event,
        'latest_reviews': latest_reviews,
        'upcoming_events': upcoming_events,
        'stats': stats,
        'team_members': team_members,
    })
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
from django.shortcuts import render, redirect
from django.db.models import Q
from .models import Competency, Review, ForumPost
from accounts.models import ParticipantProfile, Region


def competencies_view(request):
    competencies = Competency.objects.all()
    # Передаём все компетенции в шаблон страницы.
    return render(request, 'festival/competencies.html', {
        'competencies': competencies
    })


def participants_view(request):
    # Сразу подтягиваем связанные данные, чтобы потом не было лишних запросов.
    participants = ParticipantProfile.objects.select_related('user', 'region').prefetch_related('application_set__competency').all()

    # Берём значения фильтров из URL, например:
    # /festival/participants/?q=иван&category=student
    search_query = request.GET.get('q', '').strip()
    competency_id = request.GET.get('competency', '').strip()
    category = request.GET.get('category', '').strip()
    region_id = request.GET.get('region', '').strip()

    # Ищем по имени, фамилии, отчеству и логину.
    if search_query:
        participants = participants.filter(
            Q(user__first_name__icontains=search_query) |
            Q(user__last_name__icontains=search_query) |
            Q(middle_name__icontains=search_query) |
            Q(user__username__icontains=search_query)
        )

    # Фильтр по выбранной компетенции.
    if competency_id:
        participants = participants.filter(application__competency_id=competency_id)

    # Фильтр по категории.
    if category:
        participants = participants.filter(category=category)

    # Фильтр по региону.
    if region_id:
        participants = participants.filter(region_id=region_id)

    # distinct нужен, чтобы участник не повторялся несколько раз.
    participants = participants.distinct()

    return render(request, 'festival/participants.html', {
        'participants': participants,
        'competencies': Competency.objects.all(),
        'regions': Region.objects.all(),
        'category_choices': ParticipantProfile.CATEGORY_CHOICES,
        'filters': {
            'q': search_query,
            'competency': competency_id,
            'category': category,
            'region': region_id,
        },
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

# 09. HTML страницы, часть 1

## `main/templates/main/home.html`

```html
{% extends 'base.html' %}

{% block title %}Главная | Фестиваль возможностей{% endblock %}
{% block description %}Главная страница фестиваля возможностей{% endblock %}

{% block content %}
<!-- Первый экран с быстрым входом в ключевые разделы сайта. -->
<section class="hero-box mb-5">
    <div class="row align-items-center g-4">
        <div class="col-lg-7">
            <span class="hero-badge">Абилимпикс • Веб-платформа фестиваля</span>
            <h1 class="display-5 fw-bold mt-3">Фестиваль возможностей</h1>
            <p class="lead">Площадка для развития, общения, профессионального роста и демонстрации талантов участников, экспертов и организаторов.</p>
            <div class="d-flex flex-wrap gap-3 mt-4">
                <a href="{% url 'competencies' %}" class="btn btn-light btn-lg">Смотреть компетенции</a>
                <a href="{% url 'participants' %}" class="btn btn-outline-light btn-lg">Участники фестиваля</a>
            </div>
        </div>
        <div class="col-lg-5">
            <!-- Справа показываем главное ближайшее событие и таймер до него. -->
            <div class="countdown-card">
                <p class="countdown-label">Ближайшее событие</p>
                {% if next_event %}
                    <h2 class="h3">{{ next_event.title }}</h2>
                    <p class="mb-2">{{ next_event.date|date:"d.m.Y" }}</p>
                    <div class="countdown-value">{{ countdown_days }}</div>
                    <p class="mb-0">дней до старта</p>
                {% else %}
                    <h2 class="h4">Дата скоро появится</h2>
                    <p class="mb-0">Добавь мероприятие в админке, и счётчик заполнится автоматически.</p>
                {% endif %}
            </div>
        </div>
    </div>
</section>

<!-- Слайдер закрывает отдельный критерий по главной странице. -->
<section class="mb-5">
    <div id="festivalCarousel" class="carousel slide shadow-sm" data-bs-ride="carousel">
        <div class="carousel-indicators">
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Слайд 1"></button>
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="1" aria-label="Слайд 2"></button>
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="2" aria-label="Слайд 3"></button>
        </div>
        <div class="carousel-inner rounded-4">
            <div class="carousel-item active">
                <div class="promo-slide promo-slide-blue">
                    <span class="promo-kicker">Участникам</span>
                    <h2>Выбери компетенцию и подай заявку</h2>
                    <p>На сайте уже есть личный кабинет, заявки, отзывы и фильтры по участникам.</p>
                    <a href="{% url 'register' %}" class="btn btn-light">Перейти к регистрации</a>
                </div>
            </div>
            <div class="carousel-item">
                <div class="promo-slide promo-slide-orange">
                    <span class="promo-kicker">Экспертам</span>
                    <h2>Следи за активностью и обратной связью</h2>
                    <p>Отзывы участников, обсуждения на форуме и список заявок помогают быстро оценить вовлечённость.</p>
                    <a href="{% url 'reviews' %}" class="btn btn-light">Смотреть отзывы</a>
                </div>
            </div>
            <div class="carousel-item">
                <div class="promo-slide promo-slide-green">
                    <span class="promo-kicker">Организаторам</span>
                    <h2>Показывай программу фестиваля на одной странице</h2>
                    <p>Главная страница выводит ближайшие мероприятия, счётчик до старта и последние отзывы из базы.</p>
                    <a href="{% url 'contacts' %}" class="btn btn-light">Связаться с оргкомитетом</a>
                </div>
            </div>
        </div>
    </div>
</section>

<!-- Блок статистики показывает, что данные подтягиваются из базы. -->
<section class="stats-strip mb-5">
    <div class="row g-3">
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.competencies }}</div>
                <div class="stats-label">Компетенций</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.participants }}</div>
                <div class="stats-label">Участников</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.applications }}</div>
                <div class="stats-label">Заявок</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.reviews }}</div>
                <div class="stats-label">Отзывов</div>
            </div>
        </div>
    </div>
</section>

<section class="mb-5">
    <div class="row g-4">
        <div class="col-lg-7">
            <!-- Ближайшие мероприятия берутся из модели Event. -->
            <div class="info-panel h-100">
                <div class="d-flex justify-content-between align-items-center mb-3">
                    <h2 class="section-title mb-0">Ближайшие мероприятия</h2>
                    <span class="text-muted small">Из базы данных</span>
                </div>
                <div class="row g-3">
                    {% for event in upcoming_events %}
                        <div class="col-md-6">
                            <div class="event-card">
                                <p class="event-date">{{ event.date|date:"d.m.Y" }}</p>
                                <h3 class="h5">{{ event.title }}</h3>
                                <p class="mb-0">{{ event.description|truncatechars:120 }}</p>
                            </div>
                        </div>
                    {% empty %}
                        <div class="col-12">
                            <div class="event-card">
                                <h3 class="h5">Мероприятия пока не добавлены</h3>
                                <p class="mb-0">Заполни раздел `Event` в админке, и анонсы появятся здесь автоматически.</p>
                            </div>
                        </div>
                    {% endfor %}
                </div>
            </div>
        </div>
        <div class="col-lg-5">
            <!-- Дополнительный блок объясняет последовательность участия. -->
            <div class="info-panel h-100">
                <h2 class="section-title">Как принять участие</h2>
                <div class="step-item">
                    <span class="step-number">1</span>
                    <div>
                        <h3 class="h6 mb-1">Зарегистрируйся</h3>
                        <p class="mb-0">Создай учётную запись и выбери свой регион и категорию.</p>
                    </div>
                </div>
                <div class="step-item">
                    <span class="step-number">2</span>
                    <div>
                        <h3 class="h6 mb-1">Подай заявку</h3>
                        <p class="mb-0">В личном кабинете отправь заявку на нужную компетенцию.</p>
                    </div>
                </div>
                <div class="step-item">
                    <span class="step-number">3</span>
                    <div>
                        <h3 class="h6 mb-1">Оставь отзыв</h3>
                        <p class="mb-0">После участия оцени компетенцию и поделись впечатлением.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<section class="mb-5">
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h2 class="section-title mb-0">Последние отзывы</h2>
        <a href="{% url 'reviews' %}" class="btn btn-outline-primary btn-sm">Все отзывы</a>
    </div>
    <div class="row g-4">
        {% for review in latest_reviews %}
            <div class="col-md-6 col-xl-3">
                <div class="review-preview-card h-100">
                    <div class="review-score">{{ review.rating }}/5</div>
                    <h3 class="h6 mt-3 mb-1">
                        {% if review.profile.user.last_name or review.profile.user.first_name %}
                            {{ review.profile.user.last_name }} {{ review.profile.user.first_name }}
                        {% else %}
                            {{ review.profile.user.username }}
                        {% endif %}
                    </h3>
                    <p class="text-muted small mb-2">{{ review.competency.title }}</p>
                    <p class="mb-0">{{ review.comment|truncatechars:110 }}</p>
                </div>
            </div>
        {% empty %}
            <div class="col-12">
                <div class="info-panel">
                    <p class="mb-0">Отзывов пока нет. После отправки из личного кабинета четыре последних автоматически появятся на главной.</p>
                </div>
            </div>
        {% endfor %}
    </div>
</section>

<section>
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h2 class="section-title mb-0">Команда фестиваля</h2>
        <span class="text-muted small">Организаторы и сопровождение</span>
    </div>
    <div class="row g-4">
        {% for member in team_members %}
            <div class="col-md-4">
                <div class="team-card h-100">
                    <div class="team-avatar">{{ member.name|slice:":1" }}</div>
                    <h3 class="h5 mb-1">{{ member.name }}</h3>
                    <p class="team-role">{{ member.role }}</p>
                    <p class="mb-0">{{ member.description }}</p>
                </div>
            </div>
        {% endfor %}
    </div>
</section>
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

---

# 10. HTML страницы, часть 2

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

<div class="card shadow-sm mb-4">
    <div class="card-body">
        <form method="get" class="row g-3">
            <!-- Поле поиска по имени, фамилии и логину -->
            <div class="col-md-6">
                <label class="form-label">Поиск по имени</label>
                <input type="text" name="q" value="{{ filters.q }}" class="form-control" placeholder="Имя, фамилия или логин">
            </div>

            <!-- Фильтр по компетенции -->
            <div class="col-md-6">
                <label class="form-label">Компетенция</label>
                <select name="competency" class="form-select">
                    <option value="">Все компетенции</option>
                    {% for competency in competencies %}
                        <option value="{{ competency.id }}" {% if filters.competency == competency.id|stringformat:"s" %}selected{% endif %}>
                            {{ competency.title }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <!-- Фильтр по категории -->
            <div class="col-md-6">
                <label class="form-label">Категория</label>
                <select name="category" class="form-select">
                    <option value="">Все категории</option>
                    {% for value, label in category_choices %}
                        <option value="{{ value }}" {% if filters.category == value %}selected{% endif %}>
                            {{ label }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <!-- Фильтр по региону -->
            <div class="col-md-6">
                <label class="form-label">Регион</label>
                <select name="region" class="form-select">
                    <option value="">Все регионы</option>
                    {% for region in regions %}
                        <option value="{{ region.id }}" {% if filters.region == region.id|stringformat:"s" %}selected{% endif %}>
                            {{ region.name }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <div class="col-12">
                <button type="submit" class="btn btn-primary">Применить фильтры</button>
                <a href="{% url 'participants' %}" class="btn btn-outline-secondary">Сбросить</a>
            </div>
        </form>
    </div>
</div>

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
                    <p class="mb-1">
                        <strong>Компетенции:</strong>
                        {% for application in participant.application_set.all %}
                            {{ application.competency.title }}{% if not forloop.last %}, {% endif %}
                        {% empty %}
                            Пока нет заявок
                        {% endfor %}
                    </p>
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

Что это даёт:

- фильтр по имени;
- фильтр по компетенции;
- фильтр по категории;
- фильтр по региону;
- показ компетенций участника прямо на карточке.

---

# 11. HTML страницы, часть 3

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

# 12. Forms

## `accounts/forms.py`

```python
from django import forms
from django.contrib.auth.models import User
from .models import ParticipantProfile, Region


class RegisterUserForm(forms.ModelForm):
    # Эти поля добавляем поверх стандартной модели User, чтобы сразу собрать данные участника.
    password = forms.CharField(widget=forms.PasswordInput, label='Пароль')
    password2 = forms.CharField(widget=forms.PasswordInput, label='Подтверждение пароля')
    middle_name = forms.CharField(required=False, label='Отчество')
    education = forms.CharField(required=False, label='Образование')
    institution = forms.CharField(required=False, label='Учебное заведение')
    region = forms.ModelChoiceField(queryset=Region.objects.all(), required=False, label='Регион')
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
        # Здесь держим базовую конкурсную валидацию пароля.
        cleaned_data = super().clean()
        password = cleaned_data.get('password')
        password2 = cleaned_data.get('password2')

        if password and len(password) < 8:
            self.add_error('password', 'Пароль должен быть не менее 8 символов')

        if password and password2 and password != password2:
            self.add_error('password2', 'Пароли не совпадают')

        return cleaned_data
```

Что это даст:

- в форме регистрации появится поле `Регион`;
- список будет браться из модели `Region`;
- если регионы ещё не добавлены в админке, список окажется пустым.

## `festival/forms.py`

```python
from django import forms
from .models import Application, Review, ForumPost


class ApplicationForm(forms.ModelForm):
    class Meta:
        # Профиль участника подставляем во view, поэтому в форме только компетенция.
        model = Application
        fields = ['competency']
        labels = {
            'competency': 'Выберите компетенцию',
        }


class ReviewForm(forms.ModelForm):
    # В форме отзыва ограничиваем оценку диапазоном от 1 до 5.
    class Meta:
        # Отзыв потом привязывается к текущему авторизованному пользователю.
        model = Review
        fields = ['competency', 'rating', 'comment']
        labels = {
            'competency': 'Компетенция',
            'rating': 'Оценка',
            'comment': 'Комментарий',
        }
        widgets = {
            # Браузер тоже подсказывает пользователю допустимый диапазон.
            'rating': forms.NumberInput(attrs={'min': 1, 'max': 5}),
        }

    def clean_rating(self):
        # Если пользователь вручную введёт 22, форма всё равно не пропустит значение.
        rating = self.cleaned_data['rating']
        if rating < 1 or rating > 5:
            raise forms.ValidationError('Оценка должна быть от 1 до 5.')
        return rating


class ForumPostForm(forms.ModelForm):
    class Meta:
        # Автора сообщения вручную не вводим, берём его из request.user.
        model = ForumPost
        fields = ['title', 'message']
        labels = {
            'title': 'Заголовок',
            'message': 'Сообщение',
        }
```

---

# 13. Регистрация и логин

## `accounts/views.py`

Замени на это:

```python
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout
from django.contrib.auth.forms import AuthenticationForm
from .forms import RegisterUserForm
from .models import ParticipantProfile


def register_view(request):
    if request.method == 'POST':
        form = RegisterUserForm(request.POST, request.FILES)
        if form.is_valid():
            # Сначала создаём стандартного пользователя для входа в систему.
            user = form.save(commit=False)
            user.set_password(form.cleaned_data['password'])
            user.save()

            # После этого создаём профиль с дополнительными полями участника.
            ParticipantProfile.objects.create(
                user=user,
                middle_name=form.cleaned_data.get('middle_name', ''),
                education=form.cleaned_data.get('education', ''),
                institution=form.cleaned_data.get('institution', ''),
                region=form.cleaned_data.get('region'),
                category=form.cleaned_data.get('category', 'student'),
                photo=form.cleaned_data.get('photo'),
            )

            login(request, user)
            return redirect('profile')
    else:
        # При обычном открытии страницы просто показываем пустую форму.
        form = RegisterUserForm()

    return render(request, 'accounts/register.html', {'form': form})


def login_view(request):
    if request.method == 'POST':
        # AuthenticationForm сам проверяет правильность логина и пароля.
        form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            user = form.get_user()
            login(request, user)
            return redirect('profile')
    else:
        # GET-запрос только отображает форму входа.
        form = AuthenticationForm()

    return render(request, 'accounts/login.html', {'form': form})


def logout_view(request):
    # После выхода отправляем пользователя на главную страницу.
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
        <!-- form.as_p выводит все поля формы, включая регион и фото. -->
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
        <!-- Здесь используем стандартную форму входа Django. -->
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

# 14. Заявка на участие и отзыв

## Шаг 10.4. Заявка на участие

### Обнови `accounts/views.py`

```python
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth.decorators import login_required

from .forms import RegisterUserForm
from .models import ParticipantProfile
from festival.forms import ApplicationForm, ReviewForm
from festival.models import Application


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
                region=form.cleaned_data.get('region'),
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


@login_required
def profile_view(request):
    # Если профиль ещё не создан, поднимаем его автоматически.
    profile, created = ParticipantProfile.objects.get_or_create(
        user=request.user,
        defaults={
            'middle_name': '',
            'education': '',
            'institution': '',
            'category': 'student',
        }
    )

    if request.method == 'POST' and 'send_application' in request.POST:
        # Эта ветка отвечает только за отправку заявки.
        app_form = ApplicationForm(request.POST)
        review_form = ReviewForm()

        if app_form.is_valid():
            application = app_form.save(commit=False)
            application.profile = profile
            application.save()
            return redirect('profile')

    elif request.method == 'POST' and 'send_review' in request.POST:
        # Эта ветка отвечает только за отправку отзыва.
        app_form = ApplicationForm()
        review_form = ReviewForm(request.POST)

        if review_form.is_valid():
            review = review_form.save(commit=False)
            review.profile = profile
            review.save()
            return redirect('profile')
    else:
        # При обычном открытии кабинета показываем обе пустые формы.
        app_form = ApplicationForm()
        review_form = ReviewForm()

    # В кабинет выводим только заявки текущего пользователя.
    applications = Application.objects.filter(profile=profile).select_related('competency')

    return render(request, 'accounts/profile.html', {
        'app_form': app_form,
        'review_form': review_form,
        'applications': applications,
    })
```

### `accounts/templates/accounts/profile.html`

```html
{% extends 'base.html' %}
{% block title %}Личный кабинет{% endblock %}
{% block content %}
<h1 class="section-title">Личный кабинет</h1>

<div class="row g-4">
    <div class="col-md-6">
        <!-- Левая колонка: форма заявки и форма отзыва. -->
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
                <!-- Кнопка send_review нужна, чтобы view понял, что отправили именно отзыв. -->
                <form method="post">
                    {% csrf_token %}
                    {{ review_form.as_p }}
                    <button type="submit" name="send_review" class="btn btn-success">Отправить отзыв</button>
                </form>
            </div>
        </div>
    </div>

    <div class="col-md-6">
        <!-- Правая колонка: список уже созданных заявок. -->
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

Проверка после шага:

- в форме заявки кнопка должна иметь имя `send_application`;
- в форме отзыва кнопка должна иметь имя `send_review`;
- если оставить старый шаблон без этих имён, POST не попадёт в нужную ветку и запись не сохранится.

---

# 15. Сообщение на форум, финальная проверка и баллы

## Шаг 10.6. Сообщение на форум

### Обнови `festival/views.py`

```python
from django.shortcuts import render, redirect
from django.db.models import Q
from .models import Competency, Review, ForumPost
from accounts.models import ParticipantProfile, Region
from .forms import ForumPostForm


def competencies_view(request):
    # Передаём все компетенции в шаблон страницы.
    competencies = Competency.objects.all()
    return render(request, 'festival/competencies.html', {
        'competencies': competencies
    })


def participants_view(request):
    # Сразу подтягиваем связанные данные, чтобы шаблон не делал лишние запросы.
    participants = ParticipantProfile.objects.select_related('user', 'region').prefetch_related('application_set__competency').all()

    # Все фильтры приходят через GET-параметры из формы.
    search_query = request.GET.get('q', '').strip()
    competency_id = request.GET.get('competency', '').strip()
    category = request.GET.get('category', '').strip()
    region_id = request.GET.get('region', '').strip()

    if search_query:
        # Поиск работает по имени, фамилии, отчеству и логину.
        participants = participants.filter(
            Q(user__first_name__icontains=search_query) |
            Q(user__last_name__icontains=search_query) |
            Q(middle_name__icontains=search_query) |
            Q(user__username__icontains=search_query)
        )

    if competency_id:
        # Фильтрация по компетенции идёт через поданные заявки участника.
        participants = participants.filter(application__competency_id=competency_id)

    if category:
        participants = participants.filter(category=category)

    if region_id:
        participants = participants.filter(region_id=region_id)

    # distinct убирает дубли, если у участника несколько заявок.
    participants = participants.distinct()

    return render(request, 'festival/participants.html', {
        'participants': participants,
        'competencies': Competency.objects.all(),
        'regions': Region.objects.all(),
        'category_choices': ParticipantProfile.CATEGORY_CHOICES,
        'filters': {
            'q': search_query,
            'competency': competency_id,
            'category': category,
            'region': region_id,
        },
    })


def contacts_view(request):
    # Контакты пока статические, поэтому отдельная логика здесь не нужна.
    return render(request, 'festival/contacts.html')


def forum_view(request):
    if request.method == 'POST' and request.user.is_authenticated:
        form = ForumPostForm(request.POST)
        if form.is_valid():
            # Автора сообщения подставляем из текущей сессии.
            post = form.save(commit=False)
            post.user = request.user
            post.save()
            return redirect('forum')
    else:
        # При первом открытии форума показываем пустую форму.
        form = ForumPostForm()

    # Свежие сообщения выводим сверху.
    posts = ForumPost.objects.select_related('user').order_by('-created_at')
    return render(request, 'festival/forum.html', {
        'posts': posts,
        'form': form,
    })


def reviews_view(request):
    # Отзывы просто читаем из базы и показываем от новых к старым.
    reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')
    return render(request, 'festival/reviews.html', {
        'reviews': reviews
    })
```

### Обнови `festival/templates/festival/forum.html`

```html
{% extends 'base.html' %}
{% block title %}Форум{% endblock %}
{% block content %}
<h1 class="section-title">Форум</h1>

{% if user.is_authenticated %}
<!-- Только авторизованный пользователь может отправить новое сообщение. -->
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

<!-- Ниже выводим уже сохранённые сообщения форума. -->
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
