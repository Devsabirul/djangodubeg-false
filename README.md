# djangodubeg-false

Which is successful but I don't want the insecure mode in my project when it is in production. And as the proper solution [according to me] I followed the steps below.

At first, I correct the static URL,root, and dir in settings.py

STATIC_URL = '/static/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
Then collect the static files by command

python manage.py collectstatic
Now the second step, [which also provided here] At first install whitenoise in your project directory in the command line

pip install whitenoise
Then Add 'whitenoise.middleware.WhiteNoiseMiddleware' in your middleware list in settings.py.

This should be added just below the 'django.middleware.security.SecurityMiddleware' and above all the remaining middleware. So that your middleware list will look like this:-

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware', #after this line
    'whitenoise.middleware.WhiteNoiseMiddleware', #add it exactlyhere
    'django.contrib.sessions.middleware.SessionMiddleware', #before this
    '...'
]
Add 'whitenoise.runserver_nostatic' on top of your installed apps So that your installed apps list will look like this:-

INSTALLED_APPS = [
    'whitenoise.runserver_nostatic',
    'django.contrib.admin',
    'django.contrib.auth',
    '...'
]
Done, you will be able to serve static files in production now!! [I did on my local environment as well]

Just use the runserver command as always no insecure or anything needed.

python manage.py runserver
Boom!!! It's working for me. Hahaha. I know kinda childish nature but I am so happy now.

Thanks to everyone who provided answers here and help my work.
