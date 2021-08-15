# django-react-integration
## Stack
* Django
* React

### Tutorial
1. Instalamos Django
```
pip install Django
```
2. Creamos el proyecto ejecutando
```
django-admin startproject django-react
```
3. Ingresamos a la carpeta del proyecto 
```
cd django-react
```
4. Verificamos si tenemos instalado node js  

```
node --version
```  
Si lo tenemos instalado deberia dar la versión en el terminal, usualmente se encuentra instalado en Mac OS, de no ser el caso la guia de instalacion se encuentra en https://nodejs.org/en/.

5. Creamos la app de react dentro de la carpeta de nuestro proyecto de Django
```
npx create-react-app reactapp
```
La estructura de los archivos deberia ser la siguiente, tengala en consideracion para los siguientes pasos.
```
django_react
│ 
└───django_react
│   │──__init__.py
│   │──asgi.py
│   │──settings.py
│   │──urls.py
│   └──wsgi.py
└───reactapp
```
6. Nos desplazamos al directorio de la app que acabamos de crear
```
cd reactapp
```
7. Agrupamos la aplicación en archivos estáticos para producción.
```
yarn build
```

8. Modificamos /settings.py
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Importamos modulo os
```python
import os
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; En templates agregamos el path de nuestro build de la app de react
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            os.path.join(BASE_DIR, 'reactapp/build'),
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; y creamos la siguiente variable al final del archivo

```python
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'reactapp/build/static'),
]
```
9. Modificamos /urls.py

```python
from django.contrib import admin
from django.urls import path
from django.views.generic import TemplateView

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name = 'index.html'))
```
Tutorial creado por José Izam.