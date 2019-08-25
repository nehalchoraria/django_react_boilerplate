### DJANGO 

 
    • Create a virtual environment for the project using virutalenv env. 
    • Source env/bin/activate 
    • Install Django with pip install django. 
    • Start a django project by running django-admin startproject djangoReact. 
    • Change directory to the project root and create a new app with django-admin startapp polls. 
    • Add mynewapp to installed apps in settings.py. 
    • Run app with python manage.py runserver.

### REACT

    • Run npm install -g create-react-app. 
    • Create a new app with create-react-app reactapp. 
    • Copy/cut all the contents of the React app (in name-of-project folder) and paste in the root of the Django project.** 
    • Run app with npm start from the project root.
    • Run npm run build 

### SETTINGS.PY

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

TEMPLATES = [
    {
        # ...
        'DIRS': [
            os.path.join(BASE_DIR, 'build')
        ],
        # ...
    }
]
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'build/static'),
]
MIDDLEWARE = [
  # 'django.middleware.security.SecurityMiddleware',
  'whitenoise.middleware.WhiteNoiseMiddleware',
  # ...
]

STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
ALLOWED_HOSTS = ['xyz.herokuapp.com', '127.0.0.1:8000']
URLS.PY
from django.contrib import admin
from django.urls import path, re_path
from django.views.generic import TemplateView

urlpatterns = [
    path('admin/', admin.site.urls),
    # path('api/', include('mynewapp.urls')),
    re_path('.*', TemplateView.as_view(template_name='index.html')),
]

### PACKAGE.JSON

"scripts": {
"start": "react-scripts start",
"build": "react-scripts build",
"test": "react-scripts test",
"eject": "react-scripts eject",
"postinstall": "npm run build"
},
"engines": {
"node":"12.4.0",
"npm":"6.9.0"
}


** USE npm -v and node -v to find out your versions ***

### PROCFILE 
release: python manage.py migrate
web: gunicorn reactdjango.wsgi --log-file -
*** PROCFILE SHOULD START WITH CAPITAL P. ***
requirements.txt

django>=2.1.2
gunicorn==19.7.1
whitenoise==3.3.1


***Use command - Pip freeze > requirements.txt ***

runtime.txt
python-3.6.8


### HEROKU SETUP

git init
heroku git:remote -a heroku-app-name
heroku buildpacks:set heroku/python
heroku buildpacks:add --index 1 heroku/nodejs
npm i
npm run build
git add .
git commit -am "make it better"
git push heroku master











