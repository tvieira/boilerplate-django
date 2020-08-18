# Django Boilerplate

This is my [django](https://www.djangoproject.com/) boilerplate I use
for my django projects. This project is a contant working in progress
as I learn more about django.

> Initial credits go to
[Andrew Pinkham](https://github.com/jambonrose/python-web-dev-21-2)
for his awesome web development with django course on 
[Safari Books Online](https://pywebdev.com/safari-21-2/), where I
learned this project structure.

## Structure

This boilerplate is structure in the following format:

```text
├── build_docker_env.sh
├── docker
│   ├── django
│   │   ├── Dockerfile
│   │   └── entrypoint.sh
│   └── jupyter
│       ├── Dockerfile
│       └── entrypoint.sh
├── docker-compose.yaml
├── requirements.txt
└── src
    ├── config
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    └── manage.py
```

- all python source goes within ```src``` folder
- docker files that assist on development goes within ```docker```
folder
- ```docker-compose.yaml``` initiates a full-stack dev environment
- ```build_docker_env.sh``` generates environment variable for the dev environment

## What this runs

- Django 3.x
- Postgres 10.4
- Redis (latest)
- Jupyter Notebook

It also contains some django extensions installed and pre-configured.

## How-To

Clone this git repository:

```bash
git clone https://github.com/tvieira/boilerplate-django.git yourproject
```

Create the dev environment variables (it creates a file called ```.docker-env```):

```bash
cd yourproject; ./build_docker_env.sh
```

Run the docker-compose:

```bash
docker-compose up
```

You will have a 4 containers built and running and the output should
look like this:

```text
➜ docker-compose up
Creating network "yourproject_default" with the default driver
Creating volume "yourproject_postgres_data_dev" with default driver
Creating volume "yourproject_postgres_backup_dev" with default driver
Creating volume "yourproject_redis_data_dev" with default driver

... (snip) ...

postgres_1  | 2020-08-25 01:59:47.418 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres_1  | 2020-08-25 01:59:47.418 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres_1  | 2020-08-25 01:59:47.420 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2020-08-25 01:59:47.431 UTC [42] LOG:  database system was shut down at 2020-08-25 01:59:47 UTC
postgres_1  | 2020-08-25 01:59:47.433 UTC [1] LOG:  database system is ready to accept connections

... (snip) ...

jupyter_1   | [I 01:59:51.030 NotebookApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
jupyter_1   | [I 01:59:51.045 NotebookApp] Serving notebooks from local directory: /app
jupyter_1   | [I 01:59:51.045 NotebookApp] Jupyter Notebook 6.1.3 is running at:
jupyter_1   | [I 01:59:51.045 NotebookApp] http://8b2407391030:8888/?token=91f049d7bb536739298f12cadb1a6c8db56505a54b3293c0
jupyter_1   | [I 01:59:51.045 NotebookApp]  or http://127.0.0.1:8888/?token=91f049d7bb536739298f12cadb1a6c8db56505a54b3293c0
jupyter_1   | [I 01:59:51.045 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
jupyter_1   | [C 01:59:51.048 NotebookApp]

... (snip) ...

django_1    | Watching for file changes with StatReloader
django_1    | Performing system checks...
django_1    |
django_1    | System check identified no issues (0 silenced).
django_1    | August 25, 2020 - 01:59:51
django_1    | Django version 3.1, using settings 'config.settings'
django_1    | Starting development server at http://0.0.0.0:8000/
django_1    | Quit the server with CONTROL-C.

```

To delete everything and start again (useful when you want to recreate
the database and file system):

```bash
docker-compose down -v --rmi local
```

**Note:** Currently the redis container is useless. Updates to come.

**Note 2**: The current library for psycopg2 is the binary one. It
makes it easy to develop without having to install psycopg2 deps.
