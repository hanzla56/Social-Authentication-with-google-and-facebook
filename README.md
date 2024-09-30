LOGIN THROUGH GOOGLE ACCOUNTS
*->commands

STEP1:

CREATE PROJECT:

*django-admin startproject myproject
------------------------------------------------------------------
STEP2:

CREATE APP

*python manage.py startapp myapp
------------------------------------------------------------------
STEP3:

RUN THE SERVER

*python manage.py runserver
-------------------------------------------------------------------
STEP4:

RUN MIGRATTIONS

*python manage.py migrate

--------------------------------------------------------------------
STEP5:

INSTALL ALLAUTH

*pip install django-allauth
-------------------------------------------------------------------
STEP6:

 OPEN SETTINGS.PY IN MYPROJECT FOLDER
_______________
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites',   
    'myapp',   
 
    'allauth',   
    'allauth.account',  
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google', 
]
________________________
AUTHENTICATION_BACKENDS = (
 'django.contrib.auth.backends.ModelBackend',
 'allauth.account.auth_backends.AuthenticationBackend',
 )
________________________
ADD Django allauth middleware in the middleware section
    # Add the account middleware:
    "allauth.account.middleware.AccountMiddleware",
 


________________________

SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        }
    }
}
________________________

STEP7:

CREATE TEMPLATE CREATE SOCIAL_APP FOLDER AND ADD INDEX.HTML

{% load socialaccount %}
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

    <title>Google Registration</title>
  </head>
  <body>
  <div class="alert alert-primary text-center" role="alert">
LOGIN WITH GOOGLE ACCOUNT
</div>
   
  {% if user.is_authenticated %}
  <p>Welcome, {{ user.username }} !</p>
 
  {% else %}
 <div class="alert alert-danger" role="alert">
   <a href="{% provider_login_url 'google' %}" class="alert-link">Clike Here</a>Login with Google Accounts.
</div>
 
  {% endif %}


    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
  </body>
</html>


______________________
STEP8:

#ADD PATH IN URLS.PY

from django.contrib import admin
from django.shortcuts import render
from django.urls import path,include


def home(request):
    return render(request,"login.html")

#STEP 04
urlpatterns = [
    path("admin/", admin.site.urls),
    path('accounts/', include('allauth.urls')),
    path("",home,name="homepage")
]

_______________________

STEP9:

#RUN MIGRATIONS


*python manage.py makemigrations
*python manage.py migrate

_______________________
STEP10:

CREATE API CONSOLE WATCH VIDEO CAREFULLY

1.Go to this link-> https://console.developers.google.com/

2.Dashbord create a project and proceed

3.Dashbord go to Credentials  On the dropdown, choose OAuth Client ID option

4.Dashbord OAuth consent screen create external give app name and save

5.Create OAuth client ID 
Authorized Javascript origins -> http://127.0.0.1:8000
Authorized redirect URL -> http://127.0.0.1:8000/accounts/google/login/callback/

6.Get the credentails


_______________________
STEP11:
#CREATE SUPERUSER TO VIEW ADMIN PANEL

python manage.py createsuperuser

________________________



___________________

STEP12:
#Add social applications

Provider: Google
Name: Google API
Client id: 
Secret key: 

__________________
STEP13:

SET UP THE PATH IN ADMIN

__________________

STEP14:

START USING IT THANK YOU!!
