FROM python:3.5

MAINTAINER Jiri Bires <jiri.bires@ysoft.com>

RUN apt-get update -y

# Install uWSGI
RUN pip install uwsgi

# Install NGINX
ENV NGINX_VERSION 1.11.10-1~jessie

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
 && echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y ca-certificates nginx=${NGINX_VERSION} gettext-base \
 && rm -rf /var/lib/apt/lists/*
# forward logs to docker log 
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
 && ln -sf /dev/stderr /var/log/nginx/error.log

# Configure NGINX
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/conf.d/default.conf
COPY conf/nginx.conf /etc/nginx/conf.d/
COPY conf/uwsgi.ini /etc/uwsgi/

# Install and configure Supervisord
RUN apt-get update && apt-get install -y supervisor \
 && rm -rf /var/lib/apt/lists/*
COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY ./app /app
WORKDIR /app

EXPOSE 80 443

CMD ["/usr/bin/supervisord"]