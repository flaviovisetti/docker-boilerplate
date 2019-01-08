FROM python:3.7-slim

RUN apt-get update && apt-get install -y build-essential vim \
    && pip install pipenv

WORKDIR /tmp
COPY Pipfile Pipfile.lock ./
RUN pipenv install --three --dev

WORKDIR /var/www/app
COPY . ./

CMD ['flask run']
