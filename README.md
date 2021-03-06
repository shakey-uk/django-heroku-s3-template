# Django, Heroku, S3 template

#### A project template for Django 1.6.2 with a production settings to easily deploy on Heroku with statics on S3.

Tired of typing? Use [automation](https://github.com/shakey-uk/django-heroku-s3-template/wiki/provisioning)


#### Pre-requisites

- heroku account and [toolbelt](https://toolbelt.heroku.com/) installed
- git installed
- [virtualenv](https://pypi.python.org/pypi/virtualenv)
- an AWS S3 account


## Fast rundown

#### 1. Create your working environment

```
    $ mkdir hellodjango && cd hellodjango
    $ virtualenv venv --distribute
    $ source venv/bin/activate
```

#### 2. Install Django

```
    $ pip install django
```

#### 3. Create the new project using a template

```
    $ django-admin.py startproject --template=https://github.com/shakey-uk/django-heroku-s3-template/archive/master.zip --extension=py,rst,html hellodjango .
```

#### 4. Install additional dependencies for development

```
    $ pip install -r requirements/local.txt
```

#### 5. Change project_name to hellodjango in Procfile

```
    $ echo web: gunicorn hellodjango.wsgi --chdir hellodjango > Procfile
```

#### 6. Store your app in Git

```
    $ git init
    $ git add .
    $ git commit -m "initial"
```

#### 7. Deploy to Heroku

```
    $ heroku create
    $ git push heroku master
```

#### 8. Set Heroku environment

```
    $ heroku config:set DJANGO_SETTINGS_MODULE=hellodjango.settings.production
    $ heroku config:set SECRET_KEY=my_random_secret_key
    $ heroku config:set AWS_STORAGE_BUCKET_NAME=my_application_bucket
    $ heroku config:set AWS_ACCESS_KEY_ID=my_key_id
    $ heroku config:set AWS_SECRET_ACCESS_KEY=my_secret_key
    $ heroku ps:scale web=1
    $ heroku run python hellodjango/manage.py collectstatic
```

#### 9. Finally...

```
    $ heroku open
```


#### Acknowledgements
Two scoops of Django people... https://github.com/twoscoops/django-twoscoops-project
