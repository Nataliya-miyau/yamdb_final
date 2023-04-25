[![yamdb_workflow](https://github.com/Nataliya-miyau/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/Nataliya-miyau/yamdb_final/actions/workflows/yamdb_workflow.yml)

# ЯП - Спринт 16 - CI и CD проекта api_yamdb. 
## Описание
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

## Технологии
* Python
* Django
* PostgreSQL
* NGINX
* gunicorn
* Docker
* GitHub Actions
* Yandex Cloud

## Описание Workflow
Workflow состоит из четырёх шагов:

_tests_ - проверка кода на соответствие PEP8, автоматический запуск тестов.

_рush Docker image to Docker Hub_ - сборка и публикация образа на DockerHub.

_deploy_ - автоматический деплой на боевой сервер при пуше в главную ветку main.

_send_massage_ - отправка уведомления в телеграм-чат.

## Запуск проекта

### Клонирование репозитория
Склонируйте репозиторий на локальную машину:

```
git clone git@github.com:Nataliya-miyau/yamdb_final.git
```

### Установка на удаленном сервере (Ubuntu)
Выполните вход на свой удаленный сервер:

```
ssh <USERNAME>@<IP_ADDRESS>
```

Установите docker на сервер:

```
sudo apt install docker.io
```

Установите docker-compose на сервер:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Скопируйте подготовленные файлы *docker-compose.yaml* и *nginx/default.conf* из вашего проекта на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно. Введите команду из корневой папки проекта:

```
scp docker-compose.yml <username>@<host>:/home/<username>/docker-compose.yml
scp -r nginx/ <username>@<host>:/home/<username>/
```

Для работы с Workflow добавьте в Secrets GitHub переменные окружения:

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
DOCKER_PASSWORD=<пароль DockerHub>
DOCKER_USERNAME=<имя пользователя DockerHub>
USER=<username для подключения к серверу>
HOST=<IP сервера>
PASSPHRASE=<пароль для сервера, если он установлен>
SSH_KEY=<ваш SSH ключ (для получения нужна команда: cat ~/.ssh/id_rsa)>
SECRET_KEY=<SECRET_KEY>
TELEGRAM_TO=<ID своего телеграм-аккаунта>
TELEGRAM_TOKEN=<токен вашего бота>
```
После успешного деплоя зайдите на боевой сервер и выполните следующие действия:
* создаем и применяем миграции:
```
sudo docker-compose exec web python manage.py makemigrations 
sudo docker-compose exec web python manage.py migrate
```
* подгружаем статику:
```
sudo docker-compose exec web python manage.py collectstatic
```
* заполним базу данных:
```
sudo docker-compose exec web python3 manage.py loaddata fixtures.json
```
* создадим суперпользователя:
```
sudo docker-compose exec web python manage.py createsuperuser
```
Проект запущен и будет доступен по вашему IP-адресу.

Данный проект доступен по адресу: http://158.160.59.16/redoc/ (документация) и http://158.160.59.16/admin/ 

### Авторы

[Громова Наталия](https://github.com/Nataliya-miyau)

Разработчики, которые приняли участие в проекте Yamdb:

[Остапчук Дмитрий](https://github.com/WispHes)

[Голубцов Михаил](https://github.com/MikhailEGolubtsov)

