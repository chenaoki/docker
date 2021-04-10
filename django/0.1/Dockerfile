FROM python:3.5.2
MAINTAINER chenaoki <chenaoki@gmail.com>

RUN pip install --upgrade pip
RUN pip install django==1.11.4
RUN pip install djangorestframework==3.6.4
RUN pip install django-filter
RUN pip install djangorestframework-jwt==1.11.0
RUN pip install requests
RUN pip install django-cors-headers 
RUN pip install django-tables2
RUN pip install sendgrid
RUN pip install python-dotenv

RUN useradd -U docker
RUN groupmod -g 999 docker
RUN mkdir /django
RUN chown docker:docker /django

USER docker
WORKDIR /django

