# Django Docker bilerplate with Postgres
> Django docker boilerplate with Postgres database in Docker containers using Docker compose.

## Prerequisites

* Docker `docker`
* Docker compose `docker-compose`

You don't need Python and modules to run this project, however it will be needed for linting e.t.c.

## Start a new project:

First of all download this project, then run:
```bash
docker-compose run --rm django_app django-admin startproject <name> .
docker-compose run --rm django_app python manage.py startapp <name>
docker-compose run --rm django_app chmod -Rv 777 .
```

## Configure DB

Add database settings to your `settings.py`:
```python
POSTGRES_USER =     os.environ['POSTGRES_USER']      or 'postgres'
POSTGRES_PASSWORD = os.environ['POSTGRES_PASSWORD']  or 'postgres'
POSTGRES_DB =       os.environ['POSTGRES_DB']        or 'postgres'
POSTGRES_HOST =     os.environ['POSTGRES_HOST']      or 'db'
POSTGRES_PORT = int(os.environ['POSTGRES_PORT'])     or 5432

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': POSTGRES_DB,
        'USER': POSTGRES_USER,
        'PASSWORD': POSTGRES_PASSWORD,
        'HOST': POSTGRES_HOST,
        'PORT': POSTGRES_PORT,
    }
}
```

Make migrations:
```bash
docker-compose run --rm django_app python manage.py makemigrations
docker-compose run --rm django_app python manage.py migrate
```

Create admin user:
```bash
docker-compose run --rm django_app python manage.py createsuperuser
```

# Using your application

Start your application by running:
```bash
docker-compose up --build
```

Use `CTRL+C` to stop your app.