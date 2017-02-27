# python-uwsgi-nginx

Docker image for running uWSGI and NGINX in single container.

## Tags

 * [Python 3.5 _(Dockerfile)_](https://github.com/jiribires/python-uwsgi-nginx/blob/master/python3.5/Dockerfile)
 * [Python 3.6 _(Dockerfile)_](https://github.com/jiribires/python-uwsgi-nginx/blob/master/python3.6/Dockerfile)

## Description

This is base [Docker](https://www.docker.com/) image for creating [Python](https://www.python.org/) web applications.

Image is configured to run [uWSGI](https://uwsgi-docs.readthedocs.org/en/latest/) and [NGINX](http://nginx.org/en/) in a single container.

## How to use

Simply use as base for your image using ``FROM clerbo/python-uwsgi-nginx`` in your ``Dockerfile``.

Copy your application to ``/app`` and optionally provide customized NGINX or uWSGI configuration.

## Example

```Dockerfile
FROM clerbo/python-uwsgi-nginx:python3.5

# Uncomment if you want to provide customized NGINX config
# COPY conf/nginx.conf /etc/nginx/conf.d/

# Uncomment if you want to use custom uWSGI config
# COPY conf/uwsgi.ini /app/

# Copy and install Python app
# app.py in root is required with default uwsgi.ini
COPY . /app
RUN pip install -r requirements.txt \
 && pip install -r requirements.txt
```

## License

This project is licensed under the Apache license