# Python rest_framework Docker setup

_Status: Published_
_Created: 2017-11-13 02:47:28_
_Tags: Python rest Docker_

Dockerfile
<code>
FROM python:3

ENV PYTHONUNBUFFERED = 1
RUN mkdir /code
WORKDIR /code
COPY . /code/
RUN pip install -r requirements.txt
</code>

docker-compose.yml
<code>
version: '3'

services:
  web:
    build: .
    command: python src/profiles_project/manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"

</code>
<code>
docker-compose run web python src/profiles_project/manage.py migrate
</code>
<code>
docker-compose up
</code>