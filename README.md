# 01. РџРѕРґРЅСЏС‚РёРµ РїСЂРѕРµРєС‚Р°

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~3/100`

Р­С‚Рѕ РїРµСЂРІС‹Р№ С€Р°Рі. Р—РґРµСЃСЊ С‚РІРѕСЏ Р·Р°РґР°С‡Р° РїСЂРѕСЃС‚Рѕ РїРѕРґРЅСЏС‚СЊ РїСЂРѕРµРєС‚ Рё РЅРµ СЃР»РѕРјР°С‚СЊ СЃС‚Р°СЂС‚.

## РџСЂРѕРІРµСЂРєР° РёРЅСЃС‚СЂСѓРјРµРЅС‚РѕРІ

```bash
python --version
pip --version
git --version
```

## 1.1 РЎРѕР·РґР°Р№ РїР°РїРєСѓ РїСЂРѕРµРєС‚Р°

```bash
cd C:\Users\efimz\Desktop
mkdir abilympics_festival
cd abilympics_festival
```

## 1.2 РЎРѕР·РґР°Р№ РІРёСЂС‚СѓР°Р»СЊРЅРѕРµ РѕРєСЂСѓР¶РµРЅРёРµ

```bash
python -m venv venv
```

## 1.3 РђРєС‚РёРІРёСЂСѓР№ РµРіРѕ

```bash
.\venv\Scripts\Activate.ps1
```

Р•СЃР»Рё PowerShell СЂСѓРіРЅС‘С‚СЃСЏ РЅР° РїРѕР»РёС‚РёРєСѓ РІС‹РїРѕР»РЅРµРЅРёСЏ, РІС‹РїРѕР»РЅРё РѕРґРёРЅ СЂР°Р·:

```bash
Set-ExecutionPolicy -Scope Process Bypass
```

## 1.4 РџРѕСЃС‚Р°РІСЊ РЅСѓР¶РЅС‹Рµ РїР°РєРµС‚С‹

```bash
pip install django pillow
```

## 1.5 РЎРѕР·РґР°Р№ Django-РїСЂРѕРµРєС‚

```bash
django-admin startproject config .
```

## 1.6 РЎРѕР·РґР°Р№ РїСЂРёР»РѕР¶РµРЅРёСЏ

```bash
python manage.py startapp main
python manage.py startapp accounts
python manage.py startapp festival
python manage.py startapp api
```

## 1.7 Р—Р°РїСѓСЃС‚Рё СЃРµСЂРІРµСЂ РґР»СЏ РїСЂРѕРІРµСЂРєРё

```bash
python manage.py runserver
```

## Р§С‚Рѕ Р·Р°РїРѕРјРЅРёС‚СЊ

- `startproject config .`
- 4 РїСЂРёР»РѕР¶РµРЅРёСЏ: `main`, `accounts`, `festival`, `api`
- `venv` Рё `pip install django pillow`

## Р§С‚Рѕ РїСЂРѕРІРµСЂРёС‚СЊ

- РµСЃС‚СЊ `manage.py`
- РµСЃС‚СЊ РїР°РїРєР° `config`
- СЃРµСЂРІРµСЂ СЃС‚Р°СЂС‚СѓРµС‚ Р±РµР· РѕС€РёР±РєРё


---

# 02. Settings

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~7/100`

РЎРµР№С‡Р°СЃ РЅР°СЃС‚СЂР°РёРІР°РµС€СЊ РїСЂРѕРµРєС‚ С‚Р°Рє, С‡С‚РѕР±С‹ РґР°Р»СЊС€Рµ СЂР°Р±РѕС‚Р°Р»Рё С€Р°Р±Р»РѕРЅС‹, СЃС‚Р°С‚РёРєР°, РјРµРґРёР° Рё СЂРµРґРёСЂРµРєС‚С‹ РїРѕСЃР»Рµ РІС…РѕРґР°.

## 2.1 РџСЂРёРјРµРЅСЏРµРј СЃС‚Р°РЅРґР°СЂС‚РЅС‹Рµ РјРёРіСЂР°С†РёРё

```bash
python manage.py migrate
```

## 2.2 РћС‚РєСЂС‹РІР°РµРј `config/settings.py`

РќР°Р№РґРё `INSTALLED_APPS` Рё РґРѕР±Р°РІСЊ РЅР°С€Рё РїСЂРёР»РѕР¶РµРЅРёСЏ:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # РќР°С€Рё РїСЂРёР»РѕР¶РµРЅРёСЏ РїСЂРѕРµРєС‚Р°.
    'main',
    'accounts',
    'festival',
    'api',
]
```

РџСЂРѕРІРµСЂСЊ `LANGUAGE_CODE` Рё `TIME_ZONE`:

```python
LANGUAGE_CODE = 'ru-ru'
TIME_ZONE = 'Asia/Yekaterinburg'
```

РќРёР¶Рµ Р±Р»РѕРєР° `STATIC_URL` РґРѕР±Р°РІСЊ СЌС‚Рѕ:

```python
STATIC_URL = 'static/'
# РћС‚СЃСЋРґР° Django Р±СѓРґРµС‚ Р±СЂР°С‚СЊ РѕР±С‰РёРµ CSS Рё РґСЂСѓРіРёРµ СЃС‚Р°С‚РёС‡РµСЃРєРёРµ С„Р°Р№Р»С‹ РїСЂРѕРµРєС‚Р°.
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = 'media/'
# РЎСЋРґР° Р±СѓРґСѓС‚ СЃРѕС…СЂР°РЅСЏС‚СЊСЃСЏ С„РѕС‚РѕРіСЂР°С„РёРё РїСЂРѕС„РёР»РµР№ Рё С„Р°Р№Р»С‹ Р·Р°РґР°РЅРёР№.
MEDIA_ROOT = BASE_DIR / 'media'

# РџРѕСЃР»Рµ РІС…РѕРґР° РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ СЃСЂР°Р·Сѓ РѕС‚РїСЂР°РІР»СЏРµРј РІ Р»РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚.
LOGIN_REDIRECT_URL = 'profile'
LOGOUT_REDIRECT_URL = 'home'
```

## 2.3 РЎРѕР·РґР°Р№ РїР°РїРєРё

```bash
mkdir templates
mkdir static
mkdir media
```

## 2.4 РџРѕРґРєР»СЋС‡Р°РµРј РѕР±С‰СѓСЋ РїР°РїРєСѓ С€Р°Р±Р»РѕРЅРѕРІ

Р’ `config/settings.py` РЅР°Р№РґРё Р±Р»РѕРє `TEMPLATES`.

Р‘С‹Р»Рѕ:

```python
'DIRS': [],
```

РЎРґРµР»Р°Р№ С‚Р°Рє:

```python
'DIRS': [BASE_DIR / 'templates'],  # РџРѕРґРєР»СЋС‡Р°РµРј РѕР±С‰СѓСЋ РїР°РїРєСѓ СЃ Р±Р°Р·РѕРІС‹Рј С€Р°Р±Р»РѕРЅРѕРј.
```

## Р§С‚Рѕ Р·Р°РїРѕРјРЅРёС‚СЊ

- `INSTALLED_APPS`
- `STATICFILES_DIRS`
- `MEDIA_URL` Рё `MEDIA_ROOT`
- `LOGIN_REDIRECT_URL` Рё `LOGOUT_REDIRECT_URL`
- `'DIRS': [BASE_DIR / 'templates']`


---

# 03. Р“Р»Р°РІРЅС‹Рµ URL

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~12/100`

РўРµРїРµСЂСЊ С‚С‹ СЃРѕР±РёСЂР°РµС€СЊ РјР°СЂС€СЂСѓС‚РёР·Р°С†РёСЋ РїСЂРѕРµРєС‚Р°. Р­С‚Рѕ Р±Р°Р·Р°, Р±РµР· РЅРµС‘ РїРѕС‡С‚Рё РІСЃС‘ Р±СѓРґРµС‚ РїР°РґР°С‚СЊ РЅР° `404`.

## 3.1 `config/urls.py`

РџРѕР»РЅРѕСЃС‚СЊСЋ Р·Р°РјРµРЅРё СЃРѕРґРµСЂР¶РёРјРѕРµ:

```python
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    # РџРѕРґРєР»СЋС‡Р°РµРј Р°РґРјРёРЅРєСѓ, РіР»Р°РІРЅСѓСЋ СЃС‚СЂР°РЅРёС†Сѓ, Р°РєРєР°СѓРЅС‚С‹, СЂР°Р·РґРµР» С„РµСЃС‚РёРІР°Р»СЏ Рё API.
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
    path('accounts/', include('accounts.urls')),
    path('festival/', include('festival.urls')),
    path('api/', include('api.urls')),
]

if settings.DEBUG:
    # Р’Рѕ РІСЂРµРјСЏ СЂР°Р·СЂР°Р±РѕС‚РєРё СЂР°Р·СЂРµС€Р°РµРј Django РѕС‚РґР°РІР°С‚СЊ Р·Р°РіСЂСѓР¶РµРЅРЅС‹Рµ РјРµРґРёР°-С„Р°Р№Р»С‹.
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## 3.2 РЎРѕР·РґР°Р№ `urls.py` РІ РєР°Р¶РґРѕРј РїСЂРёР»РѕР¶РµРЅРёРё

### `main/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    # РљРѕСЂРЅРµРІРѕР№ Р°РґСЂРµСЃ СЃР°Р№С‚Р° РѕС‚РєСЂС‹РІР°РµС‚ РіР»Р°РІРЅСѓСЋ СЃС‚СЂР°РЅРёС†Сѓ.
    path('', views.home, name='home'),
]
```

### `accounts/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    # РњР°СЂС€СЂСѓС‚С‹ СЂРµРіРёСЃС‚СЂР°С†РёРё, РІС…РѕРґР°, РІС‹С…РѕРґР° Рё Р»РёС‡РЅРѕРіРѕ РєР°Р±РёРЅРµС‚Р°.
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
    # РћСЃРЅРѕРІРЅС‹Рµ РїСѓР±Р»РёС‡РЅС‹Рµ СЃС‚СЂР°РЅРёС†С‹ С„РµСЃС‚РёРІР°Р»СЏ.
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
    # РўРµСЃС‚РѕРІР°СЏ API-С‚РѕС‡РєР° РґР»СЏ РїСЂРѕРІРµСЂРєРё JSON-РѕС‚РІРµС‚Р°.
    path('ping/', views.ping_view, name='api_ping'),
]
```

## Р§С‚Рѕ Р·Р°РїРѕРјРЅРёС‚СЊ

- РіР»Р°РІРЅС‹Р№ СЂРѕСѓС‚РµСЂ РІ `config/urls.py`
- `include(...)` РЅР° РєР°Р¶РґРѕРµ РїСЂРёР»РѕР¶РµРЅРёРµ
- `static(settings.MEDIA_URL, ...)` РґР»СЏ РјРµРґРёР° РІ `DEBUG`


---

# 04. Р’СЂРµРјРµРЅРЅС‹Рµ views, С‡С‚РѕР±С‹ РїСЂРѕРµРєС‚ РЅРµ РїР°РґР°Р»

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~15/100`

Р­С‚Рѕ РѕС‡РµРЅСЊ РІР°Р¶РЅС‹Р№ С€Р°Рі РїРѕ Р»РѕРіРёРєРµ `README.md`: СЃРЅР°С‡Р°Р»Р° РґРµР»Р°РµС€СЊ РІСЂРµРјРµРЅРЅС‹Рµ Р·Р°РіР»СѓС€РєРё, С‡С‚РѕР±С‹ URL СѓР¶Рµ РѕС‚РєСЂС‹РІР°Р»РёСЃСЊ, Рё С‚РѕР»СЊРєРѕ РїРѕС‚РѕРј РїРµСЂРµС…РѕРґРёС€СЊ Рє РјРѕРґРµР»СЏРј Рё С€Р°Р±Р»РѕРЅР°Рј.

## `main/views.py`

```python
from django.http import HttpResponse

def home(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ Р·Р°РіР»СѓС€РєР°, С‡С‚РѕР±С‹ СЃСЂР°Р·Сѓ РїСЂРѕРІРµСЂРёС‚СЊ РјР°СЂС€СЂСѓС‚ Р±РµР· С€Р°Р±Р»РѕРЅРѕРІ.
    return HttpResponse("Р“Р»Р°РІРЅР°СЏ СЃС‚СЂР°РЅРёС†Р°")
```

## `accounts/views.py`

```python
from django.http import HttpResponse

def register_view(request):
    # Р—Р°РіР»СѓС€РєР° СЃС‚СЂР°РЅРёС†С‹ СЂРµРіРёСЃС‚СЂР°С†РёРё РґРѕ РїРѕРґРєР»СЋС‡РµРЅРёСЏ СЂРµР°Р»СЊРЅРѕРіРѕ С€Р°Р±Р»РѕРЅР°.
    return HttpResponse("Р РµРіРёСЃС‚СЂР°С†РёСЏ")

def login_view(request):
    # Р—Р°РіР»СѓС€РєР° СЃС‚СЂР°РЅРёС†С‹ РІС…РѕРґР°.
    return HttpResponse("РђРІС‚РѕСЂРёР·Р°С†РёСЏ")

def logout_view(request):
    # Р—Р°РіР»СѓС€РєР° СЃС‚СЂР°РЅРёС†С‹ РІС‹С…РѕРґР°.
    return HttpResponse("Р’С‹С…РѕРґ")

def profile_view(request):
    # Р—Р°РіР»СѓС€РєР° Р»РёС‡РЅРѕРіРѕ РєР°Р±РёРЅРµС‚Р°.
    return HttpResponse("Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚")
```

## `festival/views.py`

```python
from django.http import HttpResponse

def competencies_view(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° СЃРїРёСЃРєР° РєРѕРјРїРµС‚РµРЅС†РёР№.
    return HttpResponse("РљРѕРјРїРµС‚РµРЅС†РёРё")

def participants_view(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° СЃРїРёСЃРєР° СѓС‡Р°СЃС‚РЅРёРєРѕРІ.
    return HttpResponse("РЈС‡Р°СЃС‚РЅРёРєРё")

def contacts_view(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° РєРѕРЅС‚Р°РєС‚РѕРІ.
    return HttpResponse("РљРѕРЅС‚Р°РєС‚С‹")

def forum_view(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° С„РѕСЂСѓРјР°.
    return HttpResponse("Р¤РѕСЂСѓРј")

def reviews_view(request):
    # Р’СЂРµРјРµРЅРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° РѕС‚Р·С‹РІРѕРІ.
    return HttpResponse("РћС‚Р·С‹РІС‹")
```

## `api/views.py`

```python
from django.http import JsonResponse

def ping_view(request):
    # Р‘С‹СЃС‚СЂР°СЏ РїСЂРѕРІРµСЂРєР°, С‡С‚Рѕ API РѕС‚РІРµС‡Р°РµС‚ JSON-РґР°РЅРЅС‹РјРё.
    return JsonResponse({"status": "ok"})
```

## Р—Р°РїСѓСЃС‚Рё СЃРµСЂРІРµСЂ СЃРЅРѕРІР°

```bash
python manage.py runserver
```

РџСЂРѕРІРµСЂСЊ:

```text
http://127.0.0.1:8000/
http://127.0.0.1:8000/accounts/register/
http://127.0.0.1:8000/festival/competencies/
http://127.0.0.1:8000/api/ping/
```


---

# 05. РњРѕРґРµР»Рё

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~30/100`

Р­С‚Рѕ СѓР¶Рµ СЃРµСЂСЊС‘Р·РЅС‹Р№ РєСѓСЃРѕРє РїРѕРґ Р±Р°Р»Р»С‹, РїРѕС‚РѕРјСѓ С‡С‚Рѕ С‚СѓС‚ РїРѕСЏРІР»СЏРµС‚СЃСЏ Р±Р°Р·Р° РґР°РЅРЅС‹С…, РїСЂРѕС„РёР»Рё, Р·Р°СЏРІРєРё, РѕС‚Р·С‹РІС‹ Рё С„РѕСЂСѓРј.

## `accounts/models.py`

```python
from django.db import models
from django.contrib.auth.models import User


class Region(models.Model):
    # РЎРїСЂР°РІРѕС‡РЅРёРє СЂРµРіРёРѕРЅРѕРІ РЅСѓР¶РµРЅ РґР»СЏ РїСЂРѕС„РёР»СЏ Рё С„РёР»СЊС‚СЂР°С†РёРё СѓС‡Р°СЃС‚РЅРёРєРѕРІ.
    name = models.CharField(max_length=100, verbose_name='РќР°Р·РІР°РЅРёРµ СЂРµРіРёРѕРЅР°')

    def __str__(self):
        return self.name

    class Meta:
        verbose_name = 'Р РµРіРёРѕРЅ'
        verbose_name_plural = 'Р РµРіРёРѕРЅС‹'


class ParticipantProfile(models.Model):
    # РљР°С‚РµРіРѕСЂРёРё РїСЂРёРіРѕРґСЏС‚СЃСЏ РґР»СЏ РІС‹РІРѕРґР° РЅР° СЃР°Р№С‚Рµ Рё РґР»СЏ С„РёР»СЊС‚СЂРѕРІ.
    CATEGORY_CHOICES = [
        ('student', 'РЎС‚СѓРґРµРЅС‚'),
        ('specialist', 'РЎРїРµС†РёР°Р»РёСЃС‚'),
        ('expert', 'Р­РєСЃРїРµСЂС‚'),
    ]

    # Р’ РїСЂРѕС„РёР»Рµ Р»РµР¶Р°С‚ РґР°РЅРЅС‹Рµ, РєРѕС‚РѕСЂС‹С… РЅРµС‚ РІ СЃС‚Р°РЅРґР°СЂС‚РЅРѕР№ РјРѕРґРµР»Рё User.
    user = models.OneToOneField(User, on_delete=models.CASCADE, verbose_name='РџРѕР»СЊР·РѕРІР°С‚РµР»СЊ')
    middle_name = models.CharField(max_length=100, blank=True, verbose_name='РћС‚С‡РµСЃС‚РІРѕ')
    education = models.CharField(max_length=200, blank=True, verbose_name='РћР±СЂР°Р·РѕРІР°РЅРёРµ')
    institution = models.CharField(max_length=255, blank=True, verbose_name='РЈС‡РµР±РЅРѕРµ Р·Р°РІРµРґРµРЅРёРµ')
    region = models.ForeignKey(Region, on_delete=models.SET_NULL, null=True, blank=True, verbose_name='Р РµРіРёРѕРЅ')
    photo = models.ImageField(upload_to='profiles/', blank=True, null=True, verbose_name='Р¤РѕС‚Рѕ')
    category = models.CharField(max_length=20, choices=CATEGORY_CHOICES, default='student', verbose_name='РљР°С‚РµРіРѕСЂРёСЏ')

    def __str__(self):
        # РўР°Рє РїСЂРѕС„РёР»СЊ Р±СѓРґРµС‚ РєСЂР°СЃРёРІРѕ РѕС‚РѕР±СЂР°Р¶Р°С‚СЊСЃСЏ РІ Р°РґРјРёРЅРєРµ.
        return f'{self.user.last_name} {self.user.first_name}'

    class Meta:
        verbose_name = 'РџСЂРѕС„РёР»СЊ СѓС‡Р°СЃС‚РЅРёРєР°'
        verbose_name_plural = 'РџСЂРѕС„РёР»Рё СѓС‡Р°СЃС‚РЅРёРєРѕРІ'
```

## `festival/models.py`

```python
from django.db import models
from django.contrib.auth.models import User
from django.core.validators import MinValueValidator, MaxValueValidator
from accounts.models import ParticipantProfile


class Competency(models.Model):
    # Р—РґРµСЃСЊ С…СЂР°РЅРёРј РѕРїРёСЃР°РЅРёРµ РєРѕРјРїРµС‚РµРЅС†РёРё Рё С„Р°Р№Р» Р·Р°РґР°РЅРёСЏ РґР»СЏ СЃРєР°С‡РёРІР°РЅРёСЏ.
    title = models.CharField(max_length=200, verbose_name='РќР°Р·РІР°РЅРёРµ РєРѕРјРїРµС‚РµРЅС†РёРё')
    description = models.TextField(verbose_name='РћРїРёСЃР°РЅРёРµ')
    task_file = models.FileField(upload_to='tasks/', blank=True, null=True, verbose_name='Р¤Р°Р№Р» Р·Р°РґР°РЅРёСЏ')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'РљРѕРјРїРµС‚РµРЅС†РёСЏ'
        verbose_name_plural = 'РљРѕРјРїРµС‚РµРЅС†РёРё'


class Event(models.Model):
    # РћС‚РґРµР»СЊРЅР°СЏ РјРѕРґРµР»СЊ РјРµСЂРѕРїСЂРёСЏС‚РёР№ РЅСѓР¶РЅР° РґР»СЏ Р°РЅРѕРЅСЃРѕРІ Рё СЂР°СЃРїРёСЃР°РЅРёСЏ.
    title = models.CharField(max_length=200, verbose_name='РќР°Р·РІР°РЅРёРµ РјРµСЂРѕРїСЂРёСЏС‚РёСЏ')
    description = models.TextField(verbose_name='РћРїРёСЃР°РЅРёРµ')
    date = models.DateField(verbose_name='Р”Р°С‚Р°')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'РњРµСЂРѕРїСЂРёСЏС‚РёРµ'
        verbose_name_plural = 'РњРµСЂРѕРїСЂРёСЏС‚РёСЏ'


class Application(models.Model):
    # РЎС‚Р°С‚СѓСЃ РїРѕРјРѕРіР°РµС‚ РІРёРґРµС‚СЊ СЃРѕСЃС‚РѕСЏРЅРёРµ Р·Р°СЏРІРєРё РІ РєР°Р±РёРЅРµС‚Рµ Рё РІ Р°РґРјРёРЅРєРµ.
    STATUS_CHOICES = [
        ('new', 'РќРѕРІР°СЏ'),
        ('approved', 'РћРґРѕР±СЂРµРЅР°'),
        ('rejected', 'РћС‚РєР»РѕРЅРµРЅР°'),
    ]

    profile = models.ForeignKey(ParticipantProfile, on_delete=models.CASCADE, verbose_name='РџСЂРѕС„РёР»СЊ')
    competency = models.ForeignKey(Competency, on_delete=models.CASCADE, verbose_name='РљРѕРјРїРµС‚РµРЅС†РёСЏ')
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='new', verbose_name='РЎС‚Р°С‚СѓСЃ')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Р”Р°С‚Р° СЃРѕР·РґР°РЅРёСЏ')

    def __str__(self):
        # РЈРґРѕР±РЅР°СЏ РїРѕРґРїРёСЃСЊ РґР»СЏ СЃРїРёСЃРєР° Р·Р°СЏРІРѕРє.
        return f'{self.profile} - {self.competency}'

    class Meta:
        verbose_name = 'Р—Р°СЏРІРєР°'
        verbose_name_plural = 'Р—Р°СЏРІРєРё'


class Review(models.Model):
    # РћС‚Р·С‹РІ С…СЂР°РЅРёС‚ РѕС†РµРЅРєСѓ Рё С‚РµРєСЃС‚ РєРѕРјРјРµРЅС‚Р°СЂРёСЏ СѓС‡Р°СЃС‚РЅРёРєР°.
    profile = models.ForeignKey(ParticipantProfile, on_delete=models.CASCADE, verbose_name='РџСЂРѕС„РёР»СЊ')
    competency = models.ForeignKey(Competency, on_delete=models.CASCADE, verbose_name='РљРѕРјРїРµС‚РµРЅС†РёСЏ')
    # РћС†РµРЅРєСѓ РѕРіСЂР°РЅРёС‡РёРІР°РµРј РґРёР°РїР°Р·РѕРЅРѕРј РѕС‚ 1 РґРѕ 5.
    rating = models.PositiveSmallIntegerField(
        verbose_name='РћС†РµРЅРєР°',
        validators=[MinValueValidator(1), MaxValueValidator(5)],
    )
    comment = models.TextField(verbose_name='РљРѕРјРјРµРЅС‚Р°СЂРёР№')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Р”Р°С‚Р° СЃРѕР·РґР°РЅРёСЏ')

    def __str__(self):
        # Р’ РїРѕРґРїРёСЃРё РѕС‚Р·С‹РІР° СЃРѕС…СЂР°РЅСЏРµРј РїСЂРёРІСЏР·РєСѓ Рє Р°РІС‚РѕСЂСѓ.
        return f'РћС‚Р·С‹РІ: {self.profile}'

    class Meta:
        verbose_name = 'РћС‚Р·С‹РІ'
        verbose_name_plural = 'РћС‚Р·С‹РІС‹'


class ForumPost(models.Model):
    # РџСЂРѕСЃС‚Р°СЏ РјРѕРґРµР»СЊ С„РѕСЂСѓРјР°: Р°РІС‚РѕСЂ, Р·Р°РіРѕР»РѕРІРѕРє, С‚РµРєСЃС‚ Рё РґР°С‚Р° СЃРѕР·РґР°РЅРёСЏ.
    user = models.ForeignKey(User, on_delete=models.CASCADE, verbose_name='РџРѕР»СЊР·РѕРІР°С‚РµР»СЊ')
    title = models.CharField(max_length=200, verbose_name='Р—Р°РіРѕР»РѕРІРѕРє')
    message = models.TextField(verbose_name='РЎРѕРѕР±С‰РµРЅРёРµ')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='Р”Р°С‚Р° СЃРѕР·РґР°РЅРёСЏ')

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = 'РЎРѕРѕР±С‰РµРЅРёРµ С„РѕСЂСѓРјР°'
        verbose_name_plural = 'РЎРѕРѕР±С‰РµРЅРёСЏ С„РѕСЂСѓРјР°'
```

## РњРёРіСЂР°С†РёРё

```bash
python manage.py makemigrations accounts
python manage.py makemigrations festival
python manage.py migrate
```


---

# 06. РђРґРјРёРЅРєР°

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~38/100`

Р—РґРµСЃСЊ С‚С‹ РїРѕРґРєР»СЋС‡Р°РµС€СЊ РІСЃРµ РјРѕРґРµР»Рё Рє Р°РґРјРёРЅРєРµ, С‡С‚РѕР±С‹ Р±С‹СЃС‚СЂРѕ РЅР°РїРѕР»РЅСЏС‚СЊ Р±Р°Р·Сѓ С‡РµСЂРµР· Р±СЂР°СѓР·РµСЂ.

## `accounts/admin.py`

```python
from django.contrib import admin
from .models import Region, ParticipantProfile


@admin.register(Region)
class RegionAdmin(admin.ModelAdmin):
    # Р”Р»СЏ СЂРµРіРёРѕРЅРѕРІ РґРѕСЃС‚Р°С‚РѕС‡РЅРѕ СЃРїРёСЃРєР° Рё РїРѕРёСЃРєР° РїРѕ РЅР°Р·РІР°РЅРёСЋ.
    list_display = ('id', 'name')
    search_fields = ('name',)


@admin.register(ParticipantProfile)
class ParticipantProfileAdmin(admin.ModelAdmin):
    # РџСЂРѕС„РёР»Рё СѓРґРѕР±РЅРѕ С„РёР»СЊС‚СЂРѕРІР°С‚СЊ РїРѕ РєР°С‚РµРіРѕСЂРёРё Рё СЂРµРіРёРѕРЅСѓ.
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
    # РљРѕРјРїРµС‚РµРЅС†РёРё РёС‰РµРј РїРѕ РЅР°Р·РІР°РЅРёСЋ.
    list_display = ('id', 'title')
    search_fields = ('title',)


@admin.register(Event)
class EventAdmin(admin.ModelAdmin):
    # Р”Р»СЏ РјРµСЂРѕРїСЂРёСЏС‚РёР№ РѕС‚РґРµР»СЊРЅРѕ РІС‹РІРѕРґРёРј РґР°С‚Сѓ Рё РґРѕР±Р°РІР»СЏРµРј С„РёР»СЊС‚СЂ РїРѕ РЅРµР№.
    list_display = ('id', 'title', 'date')
    search_fields = ('title',)
    list_filter = ('date',)


@admin.register(Application)
class ApplicationAdmin(admin.ModelAdmin):
    # Р—Р°СЏРІРєРё СѓРґРѕР±РЅРѕ СЃРѕСЂС‚РёСЂРѕРІР°С‚СЊ Рё РёСЃРєР°С‚СЊ РїРѕ СѓС‡Р°СЃС‚РЅРёРєСѓ Рё РєРѕРјРїРµС‚РµРЅС†РёРё.
    list_display = ('id', 'profile', 'competency', 'status', 'created_at')
    list_filter = ('status', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(Review)
class ReviewAdmin(admin.ModelAdmin):
    # РЈ РѕС‚Р·С‹РІРѕРІ РѕСЃС‚Р°РІР»СЏРµРј С„РёР»СЊС‚СЂ РїРѕ РѕС†РµРЅРєРµ Рё РєРѕРјРїРµС‚РµРЅС†РёРё.
    list_display = ('id', 'profile', 'competency', 'rating', 'created_at')
    list_filter = ('rating', 'competency')
    search_fields = ('profile__user__first_name', 'profile__user__last_name', 'competency__title')


@admin.register(ForumPost)
class ForumPostAdmin(admin.ModelAdmin):
    # РЎРѕРѕР±С‰РµРЅРёСЏ С„РѕСЂСѓРјР° РёС‰РµРј РїРѕ Р·Р°РіРѕР»РѕРІРєСѓ Рё Р°РІС‚РѕСЂСѓ.
    list_display = ('id', 'title', 'user', 'created_at')
    search_fields = ('title', 'user__username')
```

## РЎРѕР·РґР°С‘Рј Р°РґРјРёРЅРёСЃС‚СЂР°С‚РѕСЂР°

```bash
python manage.py createsuperuser
```

## Р—Р°РїСѓСЃРєР°РµРј РїСЂРѕРµРєС‚

```bash
python manage.py runserver
```

РћС‚РєСЂС‹РІР°Р№:

```text
http://127.0.0.1:8000/admin/
```

## Р§С‚Рѕ РґР°Р»СЊС€Рµ СЂСѓРєР°РјРё РґРѕР±Р°РІРёС‚СЊ РІ Р°РґРјРёРЅРєРµ

**Р РµРіРёРѕРЅС‹**
- Р§РµР»СЏР±РёРЅСЃРєР°СЏ РѕР±Р»Р°СЃС‚СЊ
- РЎРІРµСЂРґР»РѕРІСЃРєР°СЏ РѕР±Р»Р°СЃС‚СЊ
- РўСЋРјРµРЅСЃРєР°СЏ РѕР±Р»Р°СЃС‚СЊ

Р’Р°Р¶РЅРѕ:

- СЃРЅР°С‡Р°Р»Р° РґРѕР±Р°РІСЊ СЂРµРіРёРѕРЅС‹ РІ Р°РґРјРёРЅРєРµ;
- С‚РѕР»СЊРєРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ РІ С„РѕСЂРјРµ СЂРµРіРёСЃС‚СЂР°С†РёРё РїРѕСЏРІРёС‚СЃСЏ РЅРѕСЂРјР°Р»СЊРЅС‹Р№ РІС‹РїР°РґР°СЋС‰РёР№ СЃРїРёСЃРѕРє СЂРµРіРёРѕРЅРѕРІ.

**РљРѕРјРїРµС‚РµРЅС†РёРё**
- Р’РµР±-СЂР°Р·СЂР°Р±РѕС‚РєР°
- Р“СЂР°С„РёС‡РµСЃРєРёР№ РґРёР·Р°Р№РЅ
- РћР±СЂР°Р±РѕС‚РєР° С‚РµРєСЃС‚Р°
- РџСЂРѕРіСЂР°РјРјРёСЂРѕРІР°РЅРёРµ
- РЎРµС‚РµРІРѕРµ Рё СЃРёСЃС‚РµРјРЅРѕРµ Р°РґРјРёРЅРёСЃС‚СЂРёСЂРѕРІР°РЅРёРµ

**РњРµСЂРѕРїСЂРёСЏС‚РёСЏ**
- РћС‚РєСЂС‹С‚РёРµ С„РµСЃС‚РёРІР°Р»СЏ
- РЎРѕСЂРµРІРЅРѕРІР°РЅРёСЏ РїРѕ РєРѕРјРїРµС‚РµРЅС†РёСЏРј
- Р¦РµСЂРµРјРѕРЅРёСЏ РЅР°РіСЂР°Р¶РґРµРЅРёСЏ


---

# 07. РЁР°Р±Р»РѕРЅС‹ Рё Bootstrap

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~50/100`

РўРµРїРµСЂСЊ Сѓ С‚РµР±СЏ РїРѕСЏРІР»СЏРµС‚СЃСЏ РѕР±С‰РёР№ РєР°СЂРєР°СЃ СЃР°Р№С‚Р°: РІРµСЂС…РЅРµРµ РјРµРЅСЋ, С„СѓС‚РµСЂ Рё РѕР±С‰РёР№ CSS.

## 7.1 РЎРѕР·РґР°Р№ РїР°РїРєРё С€Р°Р±Р»РѕРЅРѕРІ

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
    <title>{% block title %}Р¤РµСЃС‚РёРІР°Р»СЊ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№{% endblock %}</title>
    <meta name="description" content="{% block description %}Р’РµР±-РїСЂРёР»РѕР¶РµРЅРёРµ С„РµСЃС‚РёРІР°Р»СЏ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№{% endblock %}">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>

<!-- РћР±С‰РµРµ РјРµРЅСЋ СЃР°Р№С‚Р° РЅР°С…РѕРґРёС‚СЃСЏ РІ base.html, С‡С‚РѕР±С‹ РЅРµ РґСѓР±Р»РёСЂРѕРІР°С‚СЊ РµРіРѕ РЅР° РєР°Р¶РґРѕР№ СЃС‚СЂР°РЅРёС†Рµ. -->
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container">
        <a class="navbar-brand fw-bold" href="{% url 'home' %}">Р¤РµСЃС‚РёРІР°Р»СЊ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№</a>

        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarMain">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarMain">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                <li class="nav-item"><a class="nav-link" href="{% url 'home' %}">Р“Р»Р°РІРЅР°СЏ</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'competencies' %}">РљРѕРјРїРµС‚РµРЅС†РёРё</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'participants' %}">РЈС‡Р°СЃС‚РЅРёРєРё</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'contacts' %}">РљРѕРЅС‚Р°РєС‚С‹</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'forum' %}">Р¤РѕСЂСѓРј</a></li>
                <li class="nav-item"><a class="nav-link" href="{% url 'reviews' %}">РћС‚Р·С‹РІС‹</a></li>

                {% if user.is_authenticated %}
                    <li class="nav-item"><a class="nav-link" href="{% url 'profile' %}">Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚</a></li>
                    <li class="nav-item"><a class="nav-link" href="{% url 'logout' %}">Р’С‹С…РѕРґ</a></li>
                {% else %}
                    <li class="nav-item"><a class="nav-link" href="{% url 'register' %}">Р РµРіРёСЃС‚СЂР°С†РёСЏ</a></li>
                    <li class="nav-item"><a class="nav-link" href="{% url 'login' %}">Р’С…РѕРґ</a></li>
                {% endif %}
            </ul>
        </div>
    </div>
</nav>

<!-- Р’ СЌС‚РѕС‚ Р±Р»РѕРє Django Р±СѓРґРµС‚ РїРѕРґСЃС‚Р°РІР»СЏС‚СЊ СЃРѕРґРµСЂР¶РёРјРѕРµ РґРѕС‡РµСЂРЅРёС… С€Р°Р±Р»РѕРЅРѕРІ. -->
<main class="py-4">
    <div class="container">
        {% block content %}{% endblock %}
    </div>
</main>

<!-- РџРѕРґРІР°Р» С‚Р°РєР¶Рµ РѕР±С‰РёР№ РґР»СЏ РІСЃРµС… СЃС‚СЂР°РЅРёС† СЃР°Р№С‚Р°. -->
<footer class="bg-light border-top py-4 mt-5">
    <div class="container">
        <div class="row">
            <div class="col-md-6">
                <h5>Р¤РµСЃС‚РёРІР°Р»СЊ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№</h5>
                <p class="mb-1">РџРѕРґРґРµСЂР¶РєР° РёРЅРєР»СЋР·РёРІРЅРѕРіРѕ РѕР±СЂР°Р·РѕРІР°РЅРёСЏ Рё РїСЂРѕС„РµСЃСЃРёРѕРЅР°Р»СЊРЅРѕРіРѕ СЂРѕСЃС‚Р°.</p>
            </div>
            <div class="col-md-6 text-md-end">
                <p class="mb-1">РўРµР»РµС„РѕРЅ: +7 (900) 000-00-00</p>
                <p class="mb-1">Email: info@festival.ru</p>
                <p class="mb-0">VK В· Telegram В· RuTube</p>
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
/* Р‘Р°Р·РѕРІС‹Р№ С„РѕРЅ РґР»СЏ РІСЃРµС… СЃС‚СЂР°РЅРёС† СЃР°Р№С‚Р°. */
body {
    background-color: #f8f9fa;
}

/* Hero-Р±Р»РѕРє РІС‹РґРµР»СЏРµС‚ РїРµСЂРІСѓСЋ СЃРµРєС†РёСЋ РіР»Р°РІРЅРѕР№ СЃС‚СЂР°РЅРёС†С‹. */
.hero-box {
    background: linear-gradient(135deg, #0d6efd, #6ea8fe);
    color: white;
    padding: 60px 30px;
    border-radius: 20px;
}

/* Р•РґРёРЅС‹Р№ СЂР°РґРёСѓСЃ РґРµР»Р°РµС‚ РєР°СЂС‚РѕС‡РєРё РІРёР·СѓР°Р»СЊРЅРѕ РѕРґРёРЅР°РєРѕРІС‹РјРё. */
.card {
    border-radius: 16px;
}

/* РћР±С‰РёР№ СЃС‚РёР»СЊ Р·Р°РіРѕР»РѕРІРєРѕРІ СЃРµРєС†РёР№. */
.section-title {
    margin-bottom: 24px;
    font-weight: 700;
}
```

Р’Р°Р¶РЅРѕ:

- РїРѕСЃР»Рµ РґРѕСЂР°Р±РѕС‚РєРё РіР»Р°РІРЅРѕР№ СЃС‚СЂР°РЅРёС†С‹ РІ СЂРµР°Р»СЊРЅРѕРј РїСЂРѕРµРєС‚Рµ `static/css/style.css` СЃС‚Р°РЅРµС‚ Р±РѕР»СЊС€Рµ;
- С‚Р°Рј РїРѕСЏРІСЏС‚СЃСЏ СЃС‚РёР»Рё РґР»СЏ СЃР»Р°Р№РґРµСЂР°, СЃС‡С‘С‚С‡РёРєР°, Р±Р»РѕРєР° СЃС‚Р°С‚РёСЃС‚РёРєРё, РѕС‚Р·С‹РІРѕРІ Рё РєРѕРјР°РЅРґС‹;
- РµСЃР»Рё СѓС‡РёС€СЊ РёРјРµРЅРЅРѕ С„РёРЅР°Р»СЊРЅС‹Р№ РІР°СЂРёР°РЅС‚ РїСЂРѕРµРєС‚Р°, СЃРјРѕС‚СЂРё СѓР¶Рµ Р°РєС‚СѓР°Р»СЊРЅС‹Р№ `style.css` РёР· РїСЂРѕРµРєС‚Р°.


---

# 08. Views С‡РµСЂРµР· render

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~60/100`

Р—РґРµСЃСЊ С‚С‹ СѓР±РёСЂР°РµС€СЊ РІСЂРµРјРµРЅРЅС‹Рµ `HttpResponse` Рё РїРѕРґРєР»СЋС‡Р°РµС€СЊ РЅР°СЃС‚РѕСЏС‰РёРµ HTML-С€Р°Р±Р»РѕРЅС‹ С‡РµСЂРµР· `render`.

## `main/views.py`

```python
from django.shortcuts import render
from django.utils import timezone

from accounts.models import ParticipantProfile
from festival.models import Application, Competency, Event, Review

def home(request):
    # Р“Р»Р°РІРЅСѓСЋ СЃС‚СЂР°РЅРёС†Сѓ СЃРѕР±РёСЂР°РµРј РёР· РґР°РЅРЅС‹С… РїСЂРѕРµРєС‚Р°, Р° РЅРµ РґРµСЂР¶РёРј РµС‘ СЃС‚Р°С‚РёС‡РЅРѕР№.
    today = timezone.localdate()
    next_event = Event.objects.filter(date__gte=today).order_by('date').first()

    if next_event is None:
        # Р•СЃР»Рё Р±СѓРґСѓС‰РёС… РјРµСЂРѕРїСЂРёСЏС‚РёР№ РµС‰С‘ РЅРµС‚, Р±РµСЂС‘Рј Р±Р»РёР¶Р°Р№С€РµРµ РґРѕСЃС‚СѓРїРЅРѕРµ РёР· Р±Р°Р·С‹.
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
            'name': 'РђРЅРЅР° РЎРјРёСЂРЅРѕРІР°',
            'role': 'РљРѕРѕСЂРґРёРЅР°С‚РѕСЂ С„РµСЃС‚РёРІР°Р»СЏ',
            'description': 'РћС‚РІРµС‡Р°РµС‚ Р·Р° СЂР°СЃРїРёСЃР°РЅРёРµ, СЂРµРіРёСЃС‚СЂР°С†РёСЋ Рё СЃРІСЏР·СЊ СЃ СѓС‡Р°СЃС‚РЅРёРєР°РјРё.',
        },
        {
            'name': 'РР»СЊСЏ Р’РѕР»РєРѕРІ',
            'role': 'РўРµС…РЅРёС‡РµСЃРєРёР№ СЌРєСЃРїРµСЂС‚',
            'description': 'РЎРѕРїСЂРѕРІРѕР¶РґР°РµС‚ РєРѕРЅРєСѓСЂСЃРЅС‹Рµ РїР»РѕС‰Р°РґРєРё Рё РїСЂРѕРІРµСЂСЏРµС‚ С‚РµС…РЅРёС‡РµСЃРєСѓСЋ РіРѕС‚РѕРІРЅРѕСЃС‚СЊ.',
        },
        {
            'name': 'РњР°СЂРёСЏ Р‘РµР»РѕРІР°',
            'role': 'РљСѓСЂР°С‚РѕСЂ СѓС‡Р°СЃС‚РЅРёРєРѕРІ',
            'description': 'РџРѕРјРѕРіР°РµС‚ СЃ РЅР°РІРёРіР°С†РёРµР№ РїРѕ СЃР°Р№С‚Сѓ, Р·Р°СЏРІРєР°РјРё Рё РѕР±СЂР°С‚РЅРѕР№ СЃРІСЏР·СЊСЋ.',
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
    # РџРµСЂРµРґР°С‘Рј РІСЃРµ РєРѕРјРїРµС‚РµРЅС†РёРё РІ С€Р°Р±Р»РѕРЅ СЃС‚СЂР°РЅРёС†С‹.
    return render(request, 'festival/competencies.html', {
        'competencies': competencies
    })


def participants_view(request):
    # РЎСЂР°Р·Сѓ РїРѕРґС‚СЏРіРёРІР°РµРј СЃРІСЏР·Р°РЅРЅС‹Рµ РґР°РЅРЅС‹Рµ, С‡С‚РѕР±С‹ РїРѕС‚РѕРј РЅРµ Р±С‹Р»Рѕ Р»РёС€РЅРёС… Р·Р°РїСЂРѕСЃРѕРІ.
    participants = ParticipantProfile.objects.select_related('user', 'region').prefetch_related('application_set__competency').all()

    # Р‘РµСЂС‘Рј Р·РЅР°С‡РµРЅРёСЏ С„РёР»СЊС‚СЂРѕРІ РёР· URL, РЅР°РїСЂРёРјРµСЂ:
    # /festival/participants/?q=РёРІР°РЅ&category=student
    search_query = request.GET.get('q', '').strip()
    competency_id = request.GET.get('competency', '').strip()
    category = request.GET.get('category', '').strip()
    region_id = request.GET.get('region', '').strip()

    # РС‰РµРј РїРѕ РёРјРµРЅРё, С„Р°РјРёР»РёРё, РѕС‚С‡РµСЃС‚РІСѓ Рё Р»РѕРіРёРЅСѓ.
    if search_query:
        participants = participants.filter(
            Q(user__first_name__icontains=search_query) |
            Q(user__last_name__icontains=search_query) |
            Q(middle_name__icontains=search_query) |
            Q(user__username__icontains=search_query)
        )

    # Р¤РёР»СЊС‚СЂ РїРѕ РІС‹Р±СЂР°РЅРЅРѕР№ РєРѕРјРїРµС‚РµРЅС†РёРё.
    if competency_id:
        participants = participants.filter(application__competency_id=competency_id)

    # Р¤РёР»СЊС‚СЂ РїРѕ РєР°С‚РµРіРѕСЂРёРё.
    if category:
        participants = participants.filter(category=category)

    # Р¤РёР»СЊС‚СЂ РїРѕ СЂРµРіРёРѕРЅСѓ.
    if region_id:
        participants = participants.filter(region_id=region_id)

    # distinct РЅСѓР¶РµРЅ, С‡С‚РѕР±С‹ СѓС‡Р°СЃС‚РЅРёРє РЅРµ РїРѕРІС‚РѕСЂСЏР»СЃСЏ РЅРµСЃРєРѕР»СЊРєРѕ СЂР°Р·.
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

## Р§С‚Рѕ Р·Р°РїРѕРјРЅРёС‚СЊ

- `render(request, 'path/to/template.html')`
- `timezone.localdate()`
- `Competency.objects.all()`
- `select_related(...)`
- `order_by('-created_at')`
- С„РёР»СЊС‚СЂС‹ Р±РµСЂСѓС‚СЃСЏ С‡РµСЂРµР· `request.GET`
- РґР»СЏ РїРѕРёСЃРєР° РїРѕ РЅРµСЃРєРѕР»СЊРєРёРј РїРѕР»СЏРј СѓРґРѕР±РЅРѕ РёСЃРїРѕР»СЊР·РѕРІР°С‚СЊ `Q(...)`


---

# 09. HTML СЃС‚СЂР°РЅРёС†С‹, С‡Р°СЃС‚СЊ 1

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~66/100`

Р­С‚Рѕ РїРµСЂРІС‹Рµ С€Р°Р±Р»РѕРЅС‹, РєРѕС‚РѕСЂС‹Рµ РёРґСѓС‚ СЃСЂР°Р·Сѓ РїРѕСЃР»Рµ РїРµСЂРµС…РѕРґР° РЅР° `render`.

## `main/templates/main/home.html`

```html
{% extends 'base.html' %}

{% block title %}Р“Р»Р°РІРЅР°СЏ | Р¤РµСЃС‚РёРІР°Р»СЊ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№{% endblock %}
{% block description %}Р“Р»Р°РІРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° С„РµСЃС‚РёРІР°Р»СЏ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№{% endblock %}

{% block content %}
<!-- РџРµСЂРІС‹Р№ СЌРєСЂР°РЅ СЃ Р±С‹СЃС‚СЂС‹Рј РІС…РѕРґРѕРј РІ РєР»СЋС‡РµРІС‹Рµ СЂР°Р·РґРµР»С‹ СЃР°Р№С‚Р°. -->
<section class="hero-box mb-5">
    <div class="row align-items-center g-4">
        <div class="col-lg-7">
            <span class="hero-badge">РђР±РёР»РёРјРїРёРєСЃ вЂў Р’РµР±-РїР»Р°С‚С„РѕСЂРјР° С„РµСЃС‚РёРІР°Р»СЏ</span>
            <h1 class="display-5 fw-bold mt-3">Р¤РµСЃС‚РёРІР°Р»СЊ РІРѕР·РјРѕР¶РЅРѕСЃС‚РµР№</h1>
            <p class="lead">РџР»РѕС‰Р°РґРєР° РґР»СЏ СЂР°Р·РІРёС‚РёСЏ, РѕР±С‰РµРЅРёСЏ, РїСЂРѕС„РµСЃСЃРёРѕРЅР°Р»СЊРЅРѕРіРѕ СЂРѕСЃС‚Р° Рё РґРµРјРѕРЅСЃС‚СЂР°С†РёРё С‚Р°Р»Р°РЅС‚РѕРІ СѓС‡Р°СЃС‚РЅРёРєРѕРІ, СЌРєСЃРїРµСЂС‚РѕРІ Рё РѕСЂРіР°РЅРёР·Р°С‚РѕСЂРѕРІ.</p>
            <div class="d-flex flex-wrap gap-3 mt-4">
                <a href="{% url 'competencies' %}" class="btn btn-light btn-lg">РЎРјРѕС‚СЂРµС‚СЊ РєРѕРјРїРµС‚РµРЅС†РёРё</a>
                <a href="{% url 'participants' %}" class="btn btn-outline-light btn-lg">РЈС‡Р°СЃС‚РЅРёРєРё С„РµСЃС‚РёРІР°Р»СЏ</a>
            </div>
        </div>
        <div class="col-lg-5">
            <!-- РЎРїСЂР°РІР° РїРѕРєР°Р·С‹РІР°РµРј РіР»Р°РІРЅРѕРµ Р±Р»РёР¶Р°Р№С€РµРµ СЃРѕР±С‹С‚РёРµ Рё С‚Р°Р№РјРµСЂ РґРѕ РЅРµРіРѕ. -->
            <div class="countdown-card">
                <p class="countdown-label">Р‘Р»РёР¶Р°Р№С€РµРµ СЃРѕР±С‹С‚РёРµ</p>
                {% if next_event %}
                    <h2 class="h3">{{ next_event.title }}</h2>
                    <p class="mb-2">{{ next_event.date|date:"d.m.Y" }}</p>
                    <div class="countdown-value">{{ countdown_days }}</div>
                    <p class="mb-0">РґРЅРµР№ РґРѕ СЃС‚Р°СЂС‚Р°</p>
                {% else %}
                    <h2 class="h4">Р”Р°С‚Р° СЃРєРѕСЂРѕ РїРѕСЏРІРёС‚СЃСЏ</h2>
                    <p class="mb-0">Р”РѕР±Р°РІСЊ РјРµСЂРѕРїСЂРёСЏС‚РёРµ РІ Р°РґРјРёРЅРєРµ, Рё СЃС‡С‘С‚С‡РёРє Р·Р°РїРѕР»РЅРёС‚СЃСЏ Р°РІС‚РѕРјР°С‚РёС‡РµСЃРєРё.</p>
                {% endif %}
            </div>
        </div>
    </div>
</section>

<!-- РЎР»Р°Р№РґРµСЂ Р·Р°РєСЂС‹РІР°РµС‚ РѕС‚РґРµР»СЊРЅС‹Р№ РєСЂРёС‚РµСЂРёР№ РїРѕ РіР»Р°РІРЅРѕР№ СЃС‚СЂР°РЅРёС†Рµ. -->
<section class="mb-5">
    <div id="festivalCarousel" class="carousel slide shadow-sm" data-bs-ride="carousel">
        <div class="carousel-indicators">
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="РЎР»Р°Р№Рґ 1"></button>
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="1" aria-label="РЎР»Р°Р№Рґ 2"></button>
            <button type="button" data-bs-target="#festivalCarousel" data-bs-slide-to="2" aria-label="РЎР»Р°Р№Рґ 3"></button>
        </div>
        <div class="carousel-inner rounded-4">
            <div class="carousel-item active">
                <div class="promo-slide promo-slide-blue">
                    <span class="promo-kicker">РЈС‡Р°СЃС‚РЅРёРєР°Рј</span>
                    <h2>Р’С‹Р±РµСЂРё РєРѕРјРїРµС‚РµРЅС†РёСЋ Рё РїРѕРґР°Р№ Р·Р°СЏРІРєСѓ</h2>
                    <p>РќР° СЃР°Р№С‚Рµ СѓР¶Рµ РµСЃС‚СЊ Р»РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚, Р·Р°СЏРІРєРё, РѕС‚Р·С‹РІС‹ Рё С„РёР»СЊС‚СЂС‹ РїРѕ СѓС‡Р°СЃС‚РЅРёРєР°Рј.</p>
                    <a href="{% url 'register' %}" class="btn btn-light">РџРµСЂРµР№С‚Рё Рє СЂРµРіРёСЃС‚СЂР°С†РёРё</a>
                </div>
            </div>
            <div class="carousel-item">
                <div class="promo-slide promo-slide-orange">
                    <span class="promo-kicker">Р­РєСЃРїРµСЂС‚Р°Рј</span>
                    <h2>РЎР»РµРґРё Р·Р° Р°РєС‚РёРІРЅРѕСЃС‚СЊСЋ Рё РѕР±СЂР°С‚РЅРѕР№ СЃРІСЏР·СЊСЋ</h2>
                    <p>РћС‚Р·С‹РІС‹ СѓС‡Р°СЃС‚РЅРёРєРѕРІ, РѕР±СЃСѓР¶РґРµРЅРёСЏ РЅР° С„РѕСЂСѓРјРµ Рё СЃРїРёСЃРѕРє Р·Р°СЏРІРѕРє РїРѕРјРѕРіР°СЋС‚ Р±С‹СЃС‚СЂРѕ РѕС†РµРЅРёС‚СЊ РІРѕРІР»РµС‡С‘РЅРЅРѕСЃС‚СЊ.</p>
                    <a href="{% url 'reviews' %}" class="btn btn-light">РЎРјРѕС‚СЂРµС‚СЊ РѕС‚Р·С‹РІС‹</a>
                </div>
            </div>
            <div class="carousel-item">
                <div class="promo-slide promo-slide-green">
                    <span class="promo-kicker">РћСЂРіР°РЅРёР·Р°С‚РѕСЂР°Рј</span>
                    <h2>РџРѕРєР°Р·С‹РІР°Р№ РїСЂРѕРіСЂР°РјРјСѓ С„РµСЃС‚РёРІР°Р»СЏ РЅР° РѕРґРЅРѕР№ СЃС‚СЂР°РЅРёС†Рµ</h2>
                    <p>Р“Р»Р°РІРЅР°СЏ СЃС‚СЂР°РЅРёС†Р° РІС‹РІРѕРґРёС‚ Р±Р»РёР¶Р°Р№С€РёРµ РјРµСЂРѕРїСЂРёСЏС‚РёСЏ, СЃС‡С‘С‚С‡РёРє РґРѕ СЃС‚Р°СЂС‚Р° Рё РїРѕСЃР»РµРґРЅРёРµ РѕС‚Р·С‹РІС‹ РёР· Р±Р°Р·С‹.</p>
                    <a href="{% url 'contacts' %}" class="btn btn-light">РЎРІСЏР·Р°С‚СЊСЃСЏ СЃ РѕСЂРіРєРѕРјРёС‚РµС‚РѕРј</a>
                </div>
            </div>
        </div>
    </div>
</section>

<!-- Р‘Р»РѕРє СЃС‚Р°С‚РёСЃС‚РёРєРё РїРѕРєР°Р·С‹РІР°РµС‚, С‡С‚Рѕ РґР°РЅРЅС‹Рµ РїРѕРґС‚СЏРіРёРІР°СЋС‚СЃСЏ РёР· Р±Р°Р·С‹. -->
<section class="stats-strip mb-5">
    <div class="row g-3">
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.competencies }}</div>
                <div class="stats-label">РљРѕРјРїРµС‚РµРЅС†РёР№</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.participants }}</div>
                <div class="stats-label">РЈС‡Р°СЃС‚РЅРёРєРѕРІ</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.applications }}</div>
                <div class="stats-label">Р—Р°СЏРІРѕРє</div>
            </div>
        </div>
        <div class="col-6 col-lg-3">
            <div class="stats-card">
                <div class="stats-value">{{ stats.reviews }}</div>
                <div class="stats-label">РћС‚Р·С‹РІРѕРІ</div>
            </div>
        </div>
    </div>
</section>

<section class="mb-5">
    <div class="row g-4">
        <div class="col-lg-7">
            <!-- Р‘Р»РёР¶Р°Р№С€РёРµ РјРµСЂРѕРїСЂРёСЏС‚РёСЏ Р±РµСЂСѓС‚СЃСЏ РёР· РјРѕРґРµР»Рё Event. -->
            <div class="info-panel h-100">
                <div class="d-flex justify-content-between align-items-center mb-3">
                    <h2 class="section-title mb-0">Р‘Р»РёР¶Р°Р№С€РёРµ РјРµСЂРѕРїСЂРёСЏС‚РёСЏ</h2>
                    <span class="text-muted small">РР· Р±Р°Р·С‹ РґР°РЅРЅС‹С…</span>
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
                                <h3 class="h5">РњРµСЂРѕРїСЂРёСЏС‚РёСЏ РїРѕРєР° РЅРµ РґРѕР±Р°РІР»РµРЅС‹</h3>
                                <p class="mb-0">Р—Р°РїРѕР»РЅРё СЂР°Р·РґРµР» `Event` РІ Р°РґРјРёРЅРєРµ, Рё Р°РЅРѕРЅСЃС‹ РїРѕСЏРІСЏС‚СЃСЏ Р·РґРµСЃСЊ Р°РІС‚РѕРјР°С‚РёС‡РµСЃРєРё.</p>
                            </div>
                        </div>
                    {% endfor %}
                </div>
            </div>
        </div>
        <div class="col-lg-5">
            <!-- Р”РѕРїРѕР»РЅРёС‚РµР»СЊРЅС‹Р№ Р±Р»РѕРє РѕР±СЉСЏСЃРЅСЏРµС‚ РїРѕСЃР»РµРґРѕРІР°С‚РµР»СЊРЅРѕСЃС‚СЊ СѓС‡Р°СЃС‚РёСЏ. -->
            <div class="info-panel h-100">
                <h2 class="section-title">РљР°Рє РїСЂРёРЅСЏС‚СЊ СѓС‡Р°СЃС‚РёРµ</h2>
                <div class="step-item">
                    <span class="step-number">1</span>
                    <div>
                        <h3 class="h6 mb-1">Р—Р°СЂРµРіРёСЃС‚СЂРёСЂСѓР№СЃСЏ</h3>
                        <p class="mb-0">РЎРѕР·РґР°Р№ СѓС‡С‘С‚РЅСѓСЋ Р·Р°РїРёСЃСЊ Рё РІС‹Р±РµСЂРё СЃРІРѕР№ СЂРµРіРёРѕРЅ Рё РєР°С‚РµРіРѕСЂРёСЋ.</p>
                    </div>
                </div>
                <div class="step-item">
                    <span class="step-number">2</span>
                    <div>
                        <h3 class="h6 mb-1">РџРѕРґР°Р№ Р·Р°СЏРІРєСѓ</h3>
                        <p class="mb-0">Р’ Р»РёС‡РЅРѕРј РєР°Р±РёРЅРµС‚Рµ РѕС‚РїСЂР°РІСЊ Р·Р°СЏРІРєСѓ РЅР° РЅСѓР¶РЅСѓСЋ РєРѕРјРїРµС‚РµРЅС†РёСЋ.</p>
                    </div>
                </div>
                <div class="step-item">
                    <span class="step-number">3</span>
                    <div>
                        <h3 class="h6 mb-1">РћСЃС‚Р°РІСЊ РѕС‚Р·С‹РІ</h3>
                        <p class="mb-0">РџРѕСЃР»Рµ СѓС‡Р°СЃС‚РёСЏ РѕС†РµРЅРё РєРѕРјРїРµС‚РµРЅС†РёСЋ Рё РїРѕРґРµР»РёСЃСЊ РІРїРµС‡Р°С‚Р»РµРЅРёРµРј.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<section class="mb-5">
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h2 class="section-title mb-0">РџРѕСЃР»РµРґРЅРёРµ РѕС‚Р·С‹РІС‹</h2>
        <a href="{% url 'reviews' %}" class="btn btn-outline-primary btn-sm">Р’СЃРµ РѕС‚Р·С‹РІС‹</a>
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
                    <p class="mb-0">РћС‚Р·С‹РІРѕРІ РїРѕРєР° РЅРµС‚. РџРѕСЃР»Рµ РѕС‚РїСЂР°РІРєРё РёР· Р»РёС‡РЅРѕРіРѕ РєР°Р±РёРЅРµС‚Р° С‡РµС‚С‹СЂРµ РїРѕСЃР»РµРґРЅРёС… Р°РІС‚РѕРјР°С‚РёС‡РµСЃРєРё РїРѕСЏРІСЏС‚СЃСЏ РЅР° РіР»Р°РІРЅРѕР№.</p>
                </div>
            </div>
        {% endfor %}
    </div>
</section>

<section>
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h2 class="section-title mb-0">РљРѕРјР°РЅРґР° С„РµСЃС‚РёРІР°Р»СЏ</h2>
        <span class="text-muted small">РћСЂРіР°РЅРёР·Р°С‚РѕСЂС‹ Рё СЃРѕРїСЂРѕРІРѕР¶РґРµРЅРёРµ</span>
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
{% block title %}Р РµРіРёСЃС‚СЂР°С†РёСЏ{% endblock %}
{% block content %}
<h1 class="section-title">Р РµРіРёСЃС‚СЂР°С†РёСЏ</h1>
<div class="card shadow-sm"><div class="card-body"><p>Р—РґРµСЃСЊ Р±СѓРґРµС‚ С„РѕСЂРјР° СЂРµРіРёСЃС‚СЂР°С†РёРё СѓС‡Р°СЃС‚РЅРёРєР°.</p></div></div>
{% endblock %}
```

## `accounts/templates/accounts/login.html`

```html
{% extends 'base.html' %}
{% block title %}Р’С…РѕРґ{% endblock %}
{% block content %}
<h1 class="section-title">РђРІС‚РѕСЂРёР·Р°С†РёСЏ</h1>
<div class="card shadow-sm"><div class="card-body"><p>Р—РґРµСЃСЊ Р±СѓРґРµС‚ С„РѕСЂРјР° РІС…РѕРґР°.</p></div></div>
{% endblock %}
```

## `accounts/templates/accounts/logout.html`

```html
{% extends 'base.html' %}
{% block title %}Р’С‹С…РѕРґ{% endblock %}
{% block content %}
<h1 class="section-title">Р’С‹С…РѕРґ</h1>
<div class="alert alert-info">Р—РґРµСЃСЊ РїРѕР·Р¶Рµ СЃРґРµР»Р°РµРј РІС‹С…РѕРґ РёР· Р°РєРєР°СѓРЅС‚Р°.</div>
{% endblock %}
```


---

# 10. HTML СЃС‚СЂР°РЅРёС†С‹, С‡Р°СЃС‚СЊ 2

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~72/100`

Р­С‚Рѕ СЃР»РµРґСѓСЋС‰РёР№ Р±Р»РѕРє С€Р°Р±Р»РѕРЅРѕРІ РёР· `README.md`.

## `accounts/templates/accounts/profile.html`

```html
{% extends 'base.html' %}
{% block title %}Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚{% endblock %}
{% block content %}
<h1 class="section-title">Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚</h1>
<div class="card shadow-sm"><div class="card-body"><p>Р—РґРµСЃСЊ Р±СѓРґРµС‚ РїСЂРѕС„РёР»СЊ РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ, Р·Р°СЏРІРєРё Рё РѕС‚Р·С‹РІС‹.</p></div></div>
{% endblock %}
```

## `festival/templates/festival/competencies.html`

```html
{% extends 'base.html' %}
{% block title %}РљРѕРјРїРµС‚РµРЅС†РёРё{% endblock %}
{% block content %}
<h1 class="section-title">РљРѕРјРїРµС‚РµРЅС†РёРё</h1>
<div class="row g-4">
    {% for competency in competencies %}
        <div class="col-md-6">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h2 class="h5">{{ competency.title }}</h2>
                    <p>{{ competency.description }}</p>
                    {% if competency.task_file %}
                        <a href="{{ competency.task_file.url }}" class="btn btn-primary btn-sm" download>РЎРєР°С‡Р°С‚СЊ Р·Р°РґР°РЅРёРµ</a>
                    {% else %}
                        <span class="text-muted">Р¤Р°Р№Р» РїРѕРєР° РЅРµ Р·Р°РіСЂСѓР¶РµРЅ</span>
                    {% endif %}
                </div>
            </div>
        </div>
    {% empty %}
        <p>РљРѕРјРїРµС‚РµРЅС†РёРё РїРѕРєР° РЅРµ РґРѕР±Р°РІР»РµРЅС‹.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/participants.html`

```html
{% extends 'base.html' %}
{% block title %}РЈС‡Р°СЃС‚РЅРёРєРё{% endblock %}
{% block content %}
<h1 class="section-title">РЈС‡Р°СЃС‚РЅРёРєРё</h1>

<div class="card shadow-sm mb-4">
    <div class="card-body">
        <form method="get" class="row g-3">
            <!-- РџРѕР»Рµ РїРѕРёСЃРєР° РїРѕ РёРјРµРЅРё, С„Р°РјРёР»РёРё Рё Р»РѕРіРёРЅСѓ -->
            <div class="col-md-6">
                <label class="form-label">РџРѕРёСЃРє РїРѕ РёРјРµРЅРё</label>
                <input type="text" name="q" value="{{ filters.q }}" class="form-control" placeholder="РРјСЏ, С„Р°РјРёР»РёСЏ РёР»Рё Р»РѕРіРёРЅ">
            </div>

            <!-- Р¤РёР»СЊС‚СЂ РїРѕ РєРѕРјРїРµС‚РµРЅС†РёРё -->
            <div class="col-md-6">
                <label class="form-label">РљРѕРјРїРµС‚РµРЅС†РёСЏ</label>
                <select name="competency" class="form-select">
                    <option value="">Р’СЃРµ РєРѕРјРїРµС‚РµРЅС†РёРё</option>
                    {% for competency in competencies %}
                        <option value="{{ competency.id }}" {% if filters.competency == competency.id|stringformat:"s" %}selected{% endif %}>
                            {{ competency.title }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <!-- Р¤РёР»СЊС‚СЂ РїРѕ РєР°С‚РµРіРѕСЂРёРё -->
            <div class="col-md-6">
                <label class="form-label">РљР°С‚РµРіРѕСЂРёСЏ</label>
                <select name="category" class="form-select">
                    <option value="">Р’СЃРµ РєР°С‚РµРіРѕСЂРёРё</option>
                    {% for value, label in category_choices %}
                        <option value="{{ value }}" {% if filters.category == value %}selected{% endif %}>
                            {{ label }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <!-- Р¤РёР»СЊС‚СЂ РїРѕ СЂРµРіРёРѕРЅСѓ -->
            <div class="col-md-6">
                <label class="form-label">Р РµРіРёРѕРЅ</label>
                <select name="region" class="form-select">
                    <option value="">Р’СЃРµ СЂРµРіРёРѕРЅС‹</option>
                    {% for region in regions %}
                        <option value="{{ region.id }}" {% if filters.region == region.id|stringformat:"s" %}selected{% endif %}>
                            {{ region.name }}
                        </option>
                    {% endfor %}
                </select>
            </div>

            <div class="col-12">
                <button type="submit" class="btn btn-primary">РџСЂРёРјРµРЅРёС‚СЊ С„РёР»СЊС‚СЂС‹</button>
                <a href="{% url 'participants' %}" class="btn btn-outline-secondary">РЎР±СЂРѕСЃРёС‚СЊ</a>
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
                        <img src="{{ participant.photo.url }}" alt="Р¤РѕС‚Рѕ СѓС‡Р°СЃС‚РЅРёРєР°" class="img-fluid rounded mb-3">
                    {% endif %}
                    <h2 class="h5">{{ participant.user.last_name }} {{ participant.user.first_name }} {{ participant.middle_name }}</h2>
                    <p class="mb-1"><strong>РљР°С‚РµРіРѕСЂРёСЏ:</strong> {{ participant.get_category_display }}</p>
                    <p class="mb-1"><strong>Р РµРіРёРѕРЅ:</strong> {{ participant.region }}</p>
                    <p class="mb-1">
                        <strong>РљРѕРјРїРµС‚РµРЅС†РёРё:</strong>
                        {% for application in participant.application_set.all %}
                            {{ application.competency.title }}{% if not forloop.last %}, {% endif %}
                        {% empty %}
                            РџРѕРєР° РЅРµС‚ Р·Р°СЏРІРѕРє
                        {% endfor %}
                    </p>
                    <p class="mb-1"><strong>РћР±СЂР°Р·РѕРІР°РЅРёРµ:</strong> {{ participant.education }}</p>
                    <p class="mb-0"><strong>РЈС‡СЂРµР¶РґРµРЅРёРµ:</strong> {{ participant.institution }}</p>
                </div>
            </div>
        </div>
    {% empty %}
        <p>РЈС‡Р°СЃС‚РЅРёРєРё РїРѕРєР° РЅРµ РґРѕР±Р°РІР»РµРЅС‹.</p>
    {% endfor %}
</div>
{% endblock %}
```

Р§С‚Рѕ СЌС‚Рѕ РґР°С‘С‚:

- С„РёР»СЊС‚СЂ РїРѕ РёРјРµРЅРё;
- С„РёР»СЊС‚СЂ РїРѕ РєРѕРјРїРµС‚РµРЅС†РёРё;
- С„РёР»СЊС‚СЂ РїРѕ РєР°С‚РµРіРѕСЂРёРё;
- С„РёР»СЊС‚СЂ РїРѕ СЂРµРіРёРѕРЅСѓ;
- РїРѕРєР°Р· РєРѕРјРїРµС‚РµРЅС†РёР№ СѓС‡Р°СЃС‚РЅРёРєР° РїСЂСЏРјРѕ РЅР° РєР°СЂС‚РѕС‡РєРµ.


---

# 11. HTML СЃС‚СЂР°РЅРёС†С‹, С‡Р°СЃС‚СЊ 3

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~76/100`

Р—РґРµСЃСЊ Р·Р°РІРµСЂС€Р°РµС‚СЃСЏ Р±Р°Р·РѕРІС‹Р№ Р±Р»РѕРє HTML-СЃС‚СЂР°РЅРёС† РґРѕ РїРµСЂРµС…РѕРґР° РЅР° С„РѕСЂРјС‹.

## `festival/templates/festival/contacts.html`

```html
{% extends 'base.html' %}
{% block title %}РљРѕРЅС‚Р°РєС‚С‹{% endblock %}
{% block content %}
<h1 class="section-title">РљРѕРЅС‚Р°РєС‚С‹</h1>
<div class="card shadow-sm"><div class="card-body"><p><strong>РўРµР»РµС„РѕРЅ:</strong> +7 (900) 000-00-00</p><p><strong>Email:</strong> info@festival.ru</p><p><strong>РЎРѕС†СЃРµС‚Рё:</strong> VK, Telegram, RuTube</p></div></div>
{% endblock %}
```

## `festival/templates/festival/forum.html`

```html
{% extends 'base.html' %}
{% block title %}Р¤РѕСЂСѓРј{% endblock %}
{% block content %}
<h1 class="section-title">Р¤РѕСЂСѓРј</h1>
<div class="row g-4">
    {% for post in posts %}
        <div class="col-12">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h2 class="h5">{{ post.title }}</h2>
                    <p>{{ post.message }}</p>
                    <p class="mb-1"><strong>РђРІС‚РѕСЂ:</strong> {{ post.user.username }}</p>
                    <small class="text-muted">{{ post.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>РќР° С„РѕСЂСѓРјРµ РїРѕРєР° РЅРµС‚ СЃРѕРѕР±С‰РµРЅРёР№.</p>
    {% endfor %}
</div>
{% endblock %}
```

## `festival/templates/festival/reviews.html`

```html
{% extends 'base.html' %}
{% block title %}РћС‚Р·С‹РІС‹{% endblock %}
{% block content %}
<h1 class="section-title">РћС‚Р·С‹РІС‹</h1>
<div class="row g-4">
    {% for review in reviews %}
        <div class="col-md-6">
            <div class="card shadow-sm h-100">
                <div class="card-body">
                    <h2 class="h5">{{ review.profile.user.last_name }} {{ review.profile.user.first_name }}</h2>
                    <p class="mb-1"><strong>РљРѕРјРїРµС‚РµРЅС†РёСЏ:</strong> {{ review.competency.title }}</p>
                    <p class="mb-1"><strong>РћС†РµРЅРєР°:</strong> {{ review.rating }}/5</p>
                    <p>{{ review.comment }}</p>
                    <small class="text-muted">{{ review.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>РћС‚Р·С‹РІРѕРІ РїРѕРєР° РЅРµС‚.</p>
    {% endfor %}
</div>
{% endblock %}
```


---

# 12. Forms

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~82/100`

РўРµРїРµСЂСЊ РїРѕСЏРІР»СЏСЋС‚СЃСЏ РЅР°СЃС‚РѕСЏС‰РёРµ С„РѕСЂРјС‹ РґР»СЏ СЂРµРіРёСЃС‚СЂР°С†РёРё, Р·Р°СЏРІРєРё, РѕС‚Р·С‹РІР° Рё С„РѕСЂСѓРјР°.

## `accounts/forms.py`

```python
from django import forms
from django.contrib.auth.models import User
from .models import ParticipantProfile, Region


class RegisterUserForm(forms.ModelForm):
    # Р­С‚Рё РїРѕР»СЏ РґРѕР±Р°РІР»СЏРµРј РїРѕРІРµСЂС… СЃС‚Р°РЅРґР°СЂС‚РЅРѕР№ РјРѕРґРµР»Рё User, С‡С‚РѕР±С‹ СЃСЂР°Р·Сѓ СЃРѕР±СЂР°С‚СЊ РґР°РЅРЅС‹Рµ СѓС‡Р°СЃС‚РЅРёРєР°.
    password = forms.CharField(widget=forms.PasswordInput, label='РџР°СЂРѕР»СЊ')
    password2 = forms.CharField(widget=forms.PasswordInput, label='РџРѕРґС‚РІРµСЂР¶РґРµРЅРёРµ РїР°СЂРѕР»СЏ')
    middle_name = forms.CharField(required=False, label='РћС‚С‡РµСЃС‚РІРѕ')
    education = forms.CharField(required=False, label='РћР±СЂР°Р·РѕРІР°РЅРёРµ')
    institution = forms.CharField(required=False, label='РЈС‡РµР±РЅРѕРµ Р·Р°РІРµРґРµРЅРёРµ')
    region = forms.ModelChoiceField(queryset=Region.objects.all(), required=False, label='Р РµРіРёРѕРЅ')
    category = forms.ChoiceField(choices=ParticipantProfile.CATEGORY_CHOICES, label='РљР°С‚РµРіРѕСЂРёСЏ')
    photo = forms.ImageField(required=False, label='Р¤РѕС‚Рѕ')

    class Meta:
        model = User
        fields = ['username', 'first_name', 'last_name', 'email']
        labels = {
            'username': 'Р›РѕРіРёРЅ',
            'first_name': 'РРјСЏ',
            'last_name': 'Р¤Р°РјРёР»РёСЏ',
            'email': 'Email',
        }

    def clean(self):
        # Р—РґРµСЃСЊ РґРµСЂР¶РёРј Р±Р°Р·РѕРІСѓСЋ РєРѕРЅРєСѓСЂСЃРЅСѓСЋ РІР°Р»РёРґР°С†РёСЋ РїР°СЂРѕР»СЏ.
        cleaned_data = super().clean()
        password = cleaned_data.get('password')
        password2 = cleaned_data.get('password2')

        if password and len(password) < 8:
            self.add_error('password', 'РџР°СЂРѕР»СЊ РґРѕР»Р¶РµРЅ Р±С‹С‚СЊ РЅРµ РјРµРЅРµРµ 8 СЃРёРјРІРѕР»РѕРІ')

        if password and password2 and password != password2:
            self.add_error('password2', 'РџР°СЂРѕР»Рё РЅРµ СЃРѕРІРїР°РґР°СЋС‚')

        return cleaned_data
```

Р§С‚Рѕ СЌС‚Рѕ РґР°СЃС‚:

- РІ С„РѕСЂРјРµ СЂРµРіРёСЃС‚СЂР°С†РёРё РїРѕСЏРІРёС‚СЃСЏ РїРѕР»Рµ `Р РµРіРёРѕРЅ`;
- СЃРїРёСЃРѕРє Р±СѓРґРµС‚ Р±СЂР°С‚СЊСЃСЏ РёР· РјРѕРґРµР»Рё `Region`;
- РµСЃР»Рё СЂРµРіРёРѕРЅС‹ РµС‰С‘ РЅРµ РґРѕР±Р°РІР»РµРЅС‹ РІ Р°РґРјРёРЅРєРµ, СЃРїРёСЃРѕРє РѕРєР°Р¶РµС‚СЃСЏ РїСѓСЃС‚С‹Рј.

## `festival/forms.py`

```python
from django import forms
from .models import Application, Review, ForumPost


class ApplicationForm(forms.ModelForm):
    class Meta:
        # РџСЂРѕС„РёР»СЊ СѓС‡Р°СЃС‚РЅРёРєР° РїРѕРґСЃС‚Р°РІР»СЏРµРј РІРѕ view, РїРѕСЌС‚РѕРјСѓ РІ С„РѕСЂРјРµ С‚РѕР»СЊРєРѕ РєРѕРјРїРµС‚РµРЅС†РёСЏ.
        model = Application
        fields = ['competency']
        labels = {
            'competency': 'Р’С‹Р±РµСЂРёС‚Рµ РєРѕРјРїРµС‚РµРЅС†РёСЋ',
        }


class ReviewForm(forms.ModelForm):
    # Р’ С„РѕСЂРјРµ РѕС‚Р·С‹РІР° РѕРіСЂР°РЅРёС‡РёРІР°РµРј РѕС†РµРЅРєСѓ РґРёР°РїР°Р·РѕРЅРѕРј РѕС‚ 1 РґРѕ 5.
    class Meta:
        # РћС‚Р·С‹РІ РїРѕС‚РѕРј РїСЂРёРІСЏР·С‹РІР°РµС‚СЃСЏ Рє С‚РµРєСѓС‰РµРјСѓ Р°РІС‚РѕСЂРёР·РѕРІР°РЅРЅРѕРјСѓ РїРѕР»СЊР·РѕРІР°С‚РµР»СЋ.
        model = Review
        fields = ['competency', 'rating', 'comment']
        labels = {
            'competency': 'РљРѕРјРїРµС‚РµРЅС†РёСЏ',
            'rating': 'РћС†РµРЅРєР°',
            'comment': 'РљРѕРјРјРµРЅС‚Р°СЂРёР№',
        }
        widgets = {
            # Р‘СЂР°СѓР·РµСЂ С‚РѕР¶Рµ РїРѕРґСЃРєР°Р·С‹РІР°РµС‚ РїРѕР»СЊР·РѕРІР°С‚РµР»СЋ РґРѕРїСѓСЃС‚РёРјС‹Р№ РґРёР°РїР°Р·РѕРЅ.
            'rating': forms.NumberInput(attrs={'min': 1, 'max': 5}),
        }

    def clean_rating(self):
        # Р•СЃР»Рё РїРѕР»СЊР·РѕРІР°С‚РµР»СЊ РІСЂСѓС‡РЅСѓСЋ РІРІРµРґС‘С‚ 22, С„РѕСЂРјР° РІСЃС‘ СЂР°РІРЅРѕ РЅРµ РїСЂРѕРїСѓСЃС‚РёС‚ Р·РЅР°С‡РµРЅРёРµ.
        rating = self.cleaned_data['rating']
        if rating < 1 or rating > 5:
            raise forms.ValidationError('РћС†РµРЅРєР° РґРѕР»Р¶РЅР° Р±С‹С‚СЊ РѕС‚ 1 РґРѕ 5.')
        return rating


class ForumPostForm(forms.ModelForm):
    class Meta:
        # РђРІС‚РѕСЂР° СЃРѕРѕР±С‰РµРЅРёСЏ РІСЂСѓС‡РЅСѓСЋ РЅРµ РІРІРѕРґРёРј, Р±РµСЂС‘Рј РµРіРѕ РёР· request.user.
        model = ForumPost
        fields = ['title', 'message']
        labels = {
            'title': 'Р—Р°РіРѕР»РѕРІРѕРє',
            'message': 'РЎРѕРѕР±С‰РµРЅРёРµ',
        }
```


---

# 13. Р РµРіРёСЃС‚СЂР°С†РёСЏ Рё Р»РѕРіРёРЅ

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~87/100`

Р­С‚Рѕ СѓР¶Рµ СЂР°Р±РѕС‡Р°СЏ Р°РІС‚РѕСЂРёР·Р°С†РёСЏ: СЂРµРіРёСЃС‚СЂР°С†РёСЏ РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ, СЃРѕР·РґР°РЅРёРµ РїСЂРѕС„РёР»СЏ, РІС…РѕРґ Рё РІС‹С…РѕРґ.

## `accounts/views.py`

Р—Р°РјРµРЅРё РЅР° СЌС‚Рѕ:

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
            # РЎРЅР°С‡Р°Р»Р° СЃРѕР·РґР°С‘Рј СЃС‚Р°РЅРґР°СЂС‚РЅРѕРіРѕ РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ РґР»СЏ РІС…РѕРґР° РІ СЃРёСЃС‚РµРјСѓ.
            user = form.save(commit=False)
            user.set_password(form.cleaned_data['password'])
            user.save()

            # РџРѕСЃР»Рµ СЌС‚РѕРіРѕ СЃРѕР·РґР°С‘Рј РїСЂРѕС„РёР»СЊ СЃ РґРѕРїРѕР»РЅРёС‚РµР»СЊРЅС‹РјРё РїРѕР»СЏРјРё СѓС‡Р°СЃС‚РЅРёРєР°.
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
        # РџСЂРё РѕР±С‹С‡РЅРѕРј РѕС‚РєСЂС‹С‚РёРё СЃС‚СЂР°РЅРёС†С‹ РїСЂРѕСЃС‚Рѕ РїРѕРєР°Р·С‹РІР°РµРј РїСѓСЃС‚СѓСЋ С„РѕСЂРјСѓ.
        form = RegisterUserForm()

    return render(request, 'accounts/register.html', {'form': form})


def login_view(request):
    if request.method == 'POST':
        # AuthenticationForm СЃР°Рј РїСЂРѕРІРµСЂСЏРµС‚ РїСЂР°РІРёР»СЊРЅРѕСЃС‚СЊ Р»РѕРіРёРЅР° Рё РїР°СЂРѕР»СЏ.
        form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            user = form.get_user()
            login(request, user)
            return redirect('profile')
    else:
        # GET-Р·Р°РїСЂРѕСЃ С‚РѕР»СЊРєРѕ РѕС‚РѕР±СЂР°Р¶Р°РµС‚ С„РѕСЂРјСѓ РІС…РѕРґР°.
        form = AuthenticationForm()

    return render(request, 'accounts/login.html', {'form': form})


def logout_view(request):
    # РџРѕСЃР»Рµ РІС‹С…РѕРґР° РѕС‚РїСЂР°РІР»СЏРµРј РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ РЅР° РіР»Р°РІРЅСѓСЋ СЃС‚СЂР°РЅРёС†Сѓ.
    logout(request)
    return redirect('home')


def profile_view(request):
    return render(request, 'accounts/profile.html')
```

## `accounts/templates/accounts/register.html`

```html
{% extends 'base.html' %}
{% block title %}Р РµРіРёСЃС‚СЂР°С†РёСЏ{% endblock %}
{% block content %}
<h1 class="section-title">Р РµРіРёСЃС‚СЂР°С†РёСЏ</h1>
<div class="card shadow-sm">
    <div class="card-body">
        <!-- form.as_p РІС‹РІРѕРґРёС‚ РІСЃРµ РїРѕР»СЏ С„РѕСЂРјС‹, РІРєР»СЋС‡Р°СЏ СЂРµРіРёРѕРЅ Рё С„РѕС‚Рѕ. -->
        <form method="post" enctype="multipart/form-data">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">Р—Р°СЂРµРіРёСЃС‚СЂРёСЂРѕРІР°С‚СЊСЃСЏ</button>
        </form>
    </div>
</div>
{% endblock %}
```

## `accounts/templates/accounts/login.html`

```html
{% extends 'base.html' %}
{% block title %}Р’С…РѕРґ{% endblock %}
{% block content %}
<h1 class="section-title">РђРІС‚РѕСЂРёР·Р°С†РёСЏ</h1>
<div class="card shadow-sm">
    <div class="card-body">
        <!-- Р—РґРµСЃСЊ РёСЃРїРѕР»СЊР·СѓРµРј СЃС‚Р°РЅРґР°СЂС‚РЅСѓСЋ С„РѕСЂРјСѓ РІС…РѕРґР° Django. -->
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-success">Р’РѕР№С‚Рё</button>
        </form>
    </div>
</div>
{% endblock %}
```

`logout_view` СѓР¶Рµ СЃРґРµР»Р°РЅ РІРѕ views.

Р’Р°Р¶РЅРѕ:

- РїРѕР»Рµ `region` РїРѕСЏРІРёС‚СЃСЏ РІ С€Р°Р±Р»РѕРЅРµ Р°РІС‚РѕРјР°С‚РёС‡РµСЃРєРё, РїРѕС‚РѕРјСѓ С‡С‚Рѕ РёСЃРїРѕР»СЊР·СѓРµС‚СЃСЏ `{{ form.as_p }}`;
- РЅРѕ РїРµСЂРµРґ СЌС‚РёРј РЅСѓР¶РЅРѕ РґРѕР±Р°РІРёС‚СЊ СЂРµРіРёРѕРЅС‹ РІ Р°РґРјРёРЅРєРµ, РёРЅР°С‡Рµ РІС‹РїР°РґР°СЋС‰РёР№ СЃРїРёСЃРѕРє Р±СѓРґРµС‚ РїСѓСЃС‚С‹Рј.


---

# 14. Р—Р°СЏРІРєР° РЅР° СѓС‡Р°СЃС‚РёРµ Рё РѕС‚Р·С‹РІ

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~92/100`

Р—РґРµСЃСЊ РїРѕ С€Р°РіР°Рј РґРѕСЂР°Р±Р°С‚С‹РІР°РµС‚СЃСЏ `accounts/views.py` Рё `profile.html`, С‡С‚РѕР±С‹ РІ Р»РёС‡РЅРѕРј РєР°Р±РёРЅРµС‚Рµ РјРѕР¶РЅРѕ Р±С‹Р»Рѕ РїРѕРґР°С‚СЊ Р·Р°СЏРІРєСѓ Рё РѕСЃС‚Р°РІРёС‚СЊ РѕС‚Р·С‹РІ.

Р’Р°Р¶РЅРѕ:

- С€Р°Рі `10.4` РґР°С‘С‚ РїСЂРѕРјРµР¶СѓС‚РѕС‡РЅСѓСЋ РІРµСЂСЃРёСЋ РєР°Р±РёРЅРµС‚Р°;
- РїРѕСЃР»Рµ С€Р°РіР° `10.5` РІ РїСЂРѕРµРєС‚Рµ РґРѕР»Р¶РЅР° РѕСЃС‚Р°С‚СЊСЃСЏ С‚РѕР»СЊРєРѕ С„РёРЅР°Р»СЊРЅР°СЏ РІРµСЂСЃРёСЏ `profile_view` Рё `profile.html`;
- РЅРµ РЅСѓР¶РЅРѕ РґРµСЂР¶Р°С‚СЊ РґРІРµ С„СѓРЅРєС†РёРё `profile_view` СЃСЂР°Р·Сѓ;
- РѕС‚Р·С‹РІ РІ СЌС‚РѕР№ Р»РѕРіРёРєРµ РѕСЃС‚Р°РІР»СЏРµС‚СЃСЏ РёРјРµРЅРЅРѕ РёР· Р»РёС‡РЅРѕРіРѕ РєР°Р±РёРЅРµС‚Р°, Р° СЃС‚СЂР°РЅРёС†Р° `РћС‚Р·С‹РІС‹` РїРѕС‚РѕРј РїСЂРѕСЃС‚Рѕ РїРѕРєР°Р·С‹РІР°РµС‚ СЃРѕС…СЂР°РЅС‘РЅРЅС‹Рµ Р·Р°РїРёСЃРё.

## РЁР°Рі 10.4. Р—Р°СЏРІРєР° РЅР° СѓС‡Р°СЃС‚РёРµ

### РћР±РЅРѕРІРё `accounts/views.py`

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
    # Р•СЃР»Рё РїСЂРѕС„РёР»СЊ РµС‰С‘ РЅРµ СЃРѕР·РґР°РЅ, РїРѕРґРЅРёРјР°РµРј РµРіРѕ Р°РІС‚РѕРјР°С‚РёС‡РµСЃРєРё.
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
        # Р­С‚Р° РІРµС‚РєР° РѕС‚РІРµС‡Р°РµС‚ С‚РѕР»СЊРєРѕ Р·Р° РѕС‚РїСЂР°РІРєСѓ Р·Р°СЏРІРєРё.
        app_form = ApplicationForm(request.POST)
        review_form = ReviewForm()

        if app_form.is_valid():
            application = app_form.save(commit=False)
            application.profile = profile
            application.save()
            return redirect('profile')

    elif request.method == 'POST' and 'send_review' in request.POST:
        # Р­С‚Р° РІРµС‚РєР° РѕС‚РІРµС‡Р°РµС‚ С‚РѕР»СЊРєРѕ Р·Р° РѕС‚РїСЂР°РІРєСѓ РѕС‚Р·С‹РІР°.
        app_form = ApplicationForm()
        review_form = ReviewForm(request.POST)

        if review_form.is_valid():
            review = review_form.save(commit=False)
            review.profile = profile
            review.save()
            return redirect('profile')
    else:
        # РџСЂРё РѕР±С‹С‡РЅРѕРј РѕС‚РєСЂС‹С‚РёРё РєР°Р±РёРЅРµС‚Р° РїРѕРєР°Р·С‹РІР°РµРј РѕР±Рµ РїСѓСЃС‚С‹Рµ С„РѕСЂРјС‹.
        app_form = ApplicationForm()
        review_form = ReviewForm()

    # Р’ РєР°Р±РёРЅРµС‚ РІС‹РІРѕРґРёРј С‚РѕР»СЊРєРѕ Р·Р°СЏРІРєРё С‚РµРєСѓС‰РµРіРѕ РїРѕР»СЊР·РѕРІР°С‚РµР»СЏ.
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
{% block title %}Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚{% endblock %}
{% block content %}
<h1 class="section-title">Р›РёС‡РЅС‹Р№ РєР°Р±РёРЅРµС‚</h1>

<div class="row g-4">
    <div class="col-md-6">
        <!-- Р›РµРІР°СЏ РєРѕР»РѕРЅРєР°: С„РѕСЂРјР° Р·Р°СЏРІРєРё Рё С„РѕСЂРјР° РѕС‚Р·С‹РІР°. -->
        <div class="card shadow-sm mb-4">
            <div class="card-body">
                <h2 class="h5">РџРѕРґР°С‚СЊ Р·Р°СЏРІРєСѓ</h2>
                <form method="post">
                    {% csrf_token %}
                    {{ app_form.as_p }}
                    <button type="submit" name="send_application" class="btn btn-primary">РћС‚РїСЂР°РІРёС‚СЊ Р·Р°СЏРІРєСѓ</button>
                </form>
            </div>
        </div>

        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">РћСЃС‚Р°РІРёС‚СЊ РѕС‚Р·С‹РІ</h2>
                <!-- РљРЅРѕРїРєР° send_review РЅСѓР¶РЅР°, С‡С‚РѕР±С‹ view РїРѕРЅСЏР», С‡С‚Рѕ РѕС‚РїСЂР°РІРёР»Рё РёРјРµРЅРЅРѕ РѕС‚Р·С‹РІ. -->
                <form method="post">
                    {% csrf_token %}
                    {{ review_form.as_p }}
                    <button type="submit" name="send_review" class="btn btn-success">РћС‚РїСЂР°РІРёС‚СЊ РѕС‚Р·С‹РІ</button>
                </form>
            </div>
        </div>
    </div>

    <div class="col-md-6">
        <!-- РџСЂР°РІР°СЏ РєРѕР»РѕРЅРєР°: СЃРїРёСЃРѕРє СѓР¶Рµ СЃРѕР·РґР°РЅРЅС‹С… Р·Р°СЏРІРѕРє. -->
        <div class="card shadow-sm">
            <div class="card-body">
                <h2 class="h5">РњРѕРё Р·Р°СЏРІРєРё</h2>
                {% for application in applications %}
                    <p>
                        <strong>{{ application.competency.title }}</strong><br>
                        РЎС‚Р°С‚СѓСЃ: {{ application.get_status_display }}
                    </p>
                {% empty %}
                    <p>Р—Р°СЏРІРѕРє РїРѕРєР° РЅРµС‚.</p>
                {% endfor %}
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

РџСЂРѕРІРµСЂРєР° РїРѕСЃР»Рµ С€Р°РіР°:

- РІ С„РѕСЂРјРµ Р·Р°СЏРІРєРё РєРЅРѕРїРєР° РґРѕР»Р¶РЅР° РёРјРµС‚СЊ РёРјСЏ `send_application`;
- РІ С„РѕСЂРјРµ РѕС‚Р·С‹РІР° РєРЅРѕРїРєР° РґРѕР»Р¶РЅР° РёРјРµС‚СЊ РёРјСЏ `send_review`;
- РµСЃР»Рё РѕСЃС‚Р°РІРёС‚СЊ СЃС‚Р°СЂС‹Р№ С€Р°Р±Р»РѕРЅ Р±РµР· СЌС‚РёС… РёРјС‘РЅ, POST РЅРµ РїРѕРїР°РґС‘С‚ РІ РЅСѓР¶РЅСѓСЋ РІРµС‚РєСѓ Рё Р·Р°РїРёСЃСЊ РЅРµ СЃРѕС…СЂР°РЅРёС‚СЃСЏ.


---

# 15. РЎРѕРѕР±С‰РµРЅРёРµ РЅР° С„РѕСЂСѓРј, С„РёРЅР°Р»СЊРЅР°СЏ РїСЂРѕРІРµСЂРєР° Рё Р±Р°Р»Р»С‹

РСЃС‚РѕС‡РЅРёРє: `README.md`  
РџСЂРёРјРµСЂРЅРѕ РїРѕСЃР»Рµ СЌС‚РѕРіРѕ СЌС‚Р°РїР°: `~95/100` РїРѕ Р±Р°Р·РѕРІРѕР№ Р»РѕРіРёРєРµ `README.md`

Р­С‚Рѕ РїРѕСЃР»РµРґРЅРёР№ С€Р°Рі РёР· С‚РµРєСѓС‰РµРіРѕ `README.md`.

## РЁР°Рі 10.6. РЎРѕРѕР±С‰РµРЅРёРµ РЅР° С„РѕСЂСѓРј

### РћР±РЅРѕРІРё `festival/views.py`

Р’Р°Р¶РЅРѕ:

- Р·РґРµСЃСЊ РЅСѓР¶РµРЅ РёРјРїРѕСЂС‚ `redirect`, РёРЅР°С‡Рµ РѕС‚РїСЂР°РІРєР° СЃРѕРѕР±С‰РµРЅРёСЏ РЅР° С„РѕСЂСѓРј СѓРїР°РґС‘С‚;
- СЃС‚СЂР°РЅРёС†Р° `РћС‚Р·С‹РІС‹` РІ СЌС‚РѕР№ СЃРµСЂРёРё РЅРµ СЃРѕР·РґР°С‘С‚ РѕС‚Р·С‹РІ СЃР°РјР°, РѕРЅР° С‚РѕР»СЊРєРѕ РїРѕРєР°Р·С‹РІР°РµС‚ СЃРїРёСЃРѕРє;
- РѕС‚Р·С‹РІ СЃРѕР·РґР°С‘С‚СЃСЏ РїРѕСЃР»Рµ РІС…РѕРґР° РІ `Р›РёС‡РЅРѕРј РєР°Р±РёРЅРµС‚Рµ`.

```python
from django.shortcuts import render, redirect
from django.db.models import Q
from .models import Competency, Review, ForumPost
from accounts.models import ParticipantProfile, Region
from .forms import ForumPostForm


def competencies_view(request):
    # РџРµСЂРµРґР°С‘Рј РІСЃРµ РєРѕРјРїРµС‚РµРЅС†РёРё РІ С€Р°Р±Р»РѕРЅ СЃС‚СЂР°РЅРёС†С‹.
    competencies = Competency.objects.all()
    return render(request, 'festival/competencies.html', {
        'competencies': competencies
    })


def participants_view(request):
    # РЎСЂР°Р·Сѓ РїРѕРґС‚СЏРіРёРІР°РµРј СЃРІСЏР·Р°РЅРЅС‹Рµ РґР°РЅРЅС‹Рµ, С‡С‚РѕР±С‹ С€Р°Р±Р»РѕРЅ РЅРµ РґРµР»Р°Р» Р»РёС€РЅРёРµ Р·Р°РїСЂРѕСЃС‹.
    participants = ParticipantProfile.objects.select_related('user', 'region').prefetch_related('application_set__competency').all()

    # Р’СЃРµ С„РёР»СЊС‚СЂС‹ РїСЂРёС…РѕРґСЏС‚ С‡РµСЂРµР· GET-РїР°СЂР°РјРµС‚СЂС‹ РёР· С„РѕСЂРјС‹.
    search_query = request.GET.get('q', '').strip()
    competency_id = request.GET.get('competency', '').strip()
    category = request.GET.get('category', '').strip()
    region_id = request.GET.get('region', '').strip()

    if search_query:
        # РџРѕРёСЃРє СЂР°Р±РѕС‚Р°РµС‚ РїРѕ РёРјРµРЅРё, С„Р°РјРёР»РёРё, РѕС‚С‡РµСЃС‚РІСѓ Рё Р»РѕРіРёРЅСѓ.
        participants = participants.filter(
            Q(user__first_name__icontains=search_query) |
            Q(user__last_name__icontains=search_query) |
            Q(middle_name__icontains=search_query) |
            Q(user__username__icontains=search_query)
        )

    if competency_id:
        # Р¤РёР»СЊС‚СЂР°С†РёСЏ РїРѕ РєРѕРјРїРµС‚РµРЅС†РёРё РёРґС‘С‚ С‡РµСЂРµР· РїРѕРґР°РЅРЅС‹Рµ Р·Р°СЏРІРєРё СѓС‡Р°СЃС‚РЅРёРєР°.
        participants = participants.filter(application__competency_id=competency_id)

    if category:
        participants = participants.filter(category=category)

    if region_id:
        participants = participants.filter(region_id=region_id)

    # distinct СѓР±РёСЂР°РµС‚ РґСѓР±Р»Рё, РµСЃР»Рё Сѓ СѓС‡Р°СЃС‚РЅРёРєР° РЅРµСЃРєРѕР»СЊРєРѕ Р·Р°СЏРІРѕРє.
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
    # РљРѕРЅС‚Р°РєС‚С‹ РїРѕРєР° СЃС‚Р°С‚РёС‡РµСЃРєРёРµ, РїРѕСЌС‚РѕРјСѓ РѕС‚РґРµР»СЊРЅР°СЏ Р»РѕРіРёРєР° Р·РґРµСЃСЊ РЅРµ РЅСѓР¶РЅР°.
    return render(request, 'festival/contacts.html')


def forum_view(request):
    if request.method == 'POST' and request.user.is_authenticated:
        form = ForumPostForm(request.POST)
        if form.is_valid():
            # РђРІС‚РѕСЂР° СЃРѕРѕР±С‰РµРЅРёСЏ РїРѕРґСЃС‚Р°РІР»СЏРµРј РёР· С‚РµРєСѓС‰РµР№ СЃРµСЃСЃРёРё.
            post = form.save(commit=False)
            post.user = request.user
            post.save()
            return redirect('forum')
    else:
        # РџСЂРё РїРµСЂРІРѕРј РѕС‚РєСЂС‹С‚РёРё С„РѕСЂСѓРјР° РїРѕРєР°Р·С‹РІР°РµРј РїСѓСЃС‚СѓСЋ С„РѕСЂРјСѓ.
        form = ForumPostForm()

    # РЎРІРµР¶РёРµ СЃРѕРѕР±С‰РµРЅРёСЏ РІС‹РІРѕРґРёРј СЃРІРµСЂС…Сѓ.
    posts = ForumPost.objects.select_related('user').order_by('-created_at')
    return render(request, 'festival/forum.html', {
        'posts': posts,
        'form': form,
    })


def reviews_view(request):
    # РћС‚Р·С‹РІС‹ РїСЂРѕСЃС‚Рѕ С‡РёС‚Р°РµРј РёР· Р±Р°Р·С‹ Рё РїРѕРєР°Р·С‹РІР°РµРј РѕС‚ РЅРѕРІС‹С… Рє СЃС‚Р°СЂС‹Рј.
    reviews = Review.objects.select_related('profile__user', 'competency').order_by('-created_at')
    return render(request, 'festival/reviews.html', {
        'reviews': reviews
    })
```

### РћР±РЅРѕРІРё `festival/templates/festival/forum.html`

```html
{% extends 'base.html' %}
{% block title %}Р¤РѕСЂСѓРј{% endblock %}
{% block content %}
<h1 class="section-title">Р¤РѕСЂСѓРј</h1>

{% if user.is_authenticated %}
<!-- РўРѕР»СЊРєРѕ Р°РІС‚РѕСЂРёР·РѕРІР°РЅРЅС‹Р№ РїРѕР»СЊР·РѕРІР°С‚РµР»СЊ РјРѕР¶РµС‚ РѕС‚РїСЂР°РІРёС‚СЊ РЅРѕРІРѕРµ СЃРѕРѕР±С‰РµРЅРёРµ. -->
<div class="card shadow-sm mb-4">
    <div class="card-body">
        <h2 class="h5">РќРѕРІРѕРµ СЃРѕРѕР±С‰РµРЅРёРµ</h2>
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">РћРїСѓР±Р»РёРєРѕРІР°С‚СЊ</button>
        </form>
    </div>
</div>
{% endif %}

<!-- РќРёР¶Рµ РІС‹РІРѕРґРёРј СѓР¶Рµ СЃРѕС…СЂР°РЅС‘РЅРЅС‹Рµ СЃРѕРѕР±С‰РµРЅРёСЏ С„РѕСЂСѓРјР°. -->
<div class="row g-4">
    {% for post in posts %}
        <div class="col-12">
            <div class="card shadow-sm">
                <div class="card-body">
                    <h2 class="h5">{{ post.title }}</h2>
                    <p>{{ post.message }}</p>
                    <p class="mb-1"><strong>РђРІС‚РѕСЂ:</strong> {{ post.user.username }}</p>
                    <small class="text-muted">{{ post.created_at|date:"d.m.Y H:i" }}</small>
                </div>
            </div>
        </div>
    {% empty %}
        <p>РќР° С„РѕСЂСѓРјРµ РїРѕРєР° РЅРµС‚ СЃРѕРѕР±С‰РµРЅРёР№.</p>
    {% endfor %}
</div>
{% endblock %}
```

## Р¤РёРЅР°Р»СЊРЅС‹Рµ РєРѕРјР°РЅРґС‹

```bash
python manage.py makemigrations accounts
python manage.py makemigrations festival
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## Р§С‚Рѕ РїСЂРѕРІРµСЂРёС‚СЊ РІ Р±СЂР°СѓР·РµСЂРµ

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
http://127.0.0.1:8000/api/ping/
```

## РџСЂРёРјРµСЂРЅС‹Р№ РїСЂРѕРіСЂРµСЃСЃ РїРѕ Р±Р°Р»Р»Р°Рј

- `01.md` -> `~3/100`
- `02.md` -> `~7/100`
- `03.md` -> `~12/100`
- `04.md` -> `~15/100`
- `05.md` -> `~30/100`
- `06.md` -> `~38/100`
- `07.md` -> `~50/100`
- `08.md` -> `~60/100`
- `09.md` -> `~66/100`
- `10.md` -> `~72/100`
- `11.md` -> `~76/100`
- `12.md` -> `~82/100`
- `13.md` -> `~87/100`
- `14.md` -> `~92/100`
- `15.md` -> `~95/100`

## Р’Р°Р¶РЅРѕ

Р­С‚Р° СЃРµСЂРёСЏ `01.md`-`15.md` СѓР¶Рµ РґР°С‘С‚ РѕС‡РµРЅСЊ С…РѕСЂРѕС€СѓСЋ СЂР°Р±РѕС‡СѓСЋ РѕСЃРЅРѕРІСѓ. РџРѕСЃР»Рµ РґРѕРїРѕР»РЅРёС‚РµР»СЊРЅС‹С… РґРѕСЂР°Р±РѕС‚РѕРє РІ РїСЂРѕРµРєС‚Рµ Сѓ С‚РµР±СЏ СѓР¶Рµ РµСЃС‚СЊ:

- С„РёР»СЊС‚СЂС‹ СѓС‡Р°СЃС‚РЅРёРєРѕРІ;
- РїРѕРёСЃРє РїРѕ РёРјРµРЅРё Рё РєРѕРјРїРµС‚РµРЅС†РёРё;
- СЃР»Р°Р№РґРµСЂ РЅР° РіР»Р°РІРЅРѕР№;
- СЃС‡С‘С‚С‡РёРє РґРЅРµР№ РґРѕ Р±Р»РёР¶Р°Р№С€РµРіРѕ СЃРѕР±С‹С‚РёСЏ;
- Р±Р»РѕРє РїРѕСЃР»РµРґРЅРёС… РѕС‚Р·С‹РІРѕРІ Рё РєРѕРјР°РЅРґР° С„РµСЃС‚РёРІР°Р»СЏ РЅР° РіР»Р°РІРЅРѕР№.

Р§С‚Рѕ РІСЃС‘ РµС‰С‘ РјРѕР¶РЅРѕ РґРѕР±РёС‚СЊ РѕС‚РґРµР»СЊРЅРѕ РґР»СЏ РґРѕРїРѕР»РЅРёС‚РµР»СЊРЅС‹С… Р±Р°Р»Р»РѕРІ:

- СЃРїРѕР№Р»РµСЂС‹ РёР»Рё Р°РєРєРѕСЂРґРµРѕРЅС‹ РЅР° СЃС‚СЂР°РЅРёС†Рµ РєРѕРјРїРµС‚РµРЅС†РёР№;
- С‚СѓР»С‚РёРїС‹;
- sitemap;
- Р±РѕР»РµРµ РїРѕР»РЅС‹Р№ API, Р° РЅРµ С‚РѕР»СЊРєРѕ `ping`;
- СЂРµР°Р»СЊРЅС‹Рµ С„РѕС‚Рѕ СѓС‡Р°СЃС‚РЅРёРєРѕРІ Рё С„Р°Р№Р»С‹ Р·Р°РґР°РЅРёР№ РІ Р±Р°Р·Рµ.

