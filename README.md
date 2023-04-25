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

__tests__

Проверка кода на соответствие PEP8, автоматический запуск тестов.
Push Docker image to Docker Hub
Сборка и публикация образа на DockerHub.
deploy
Автоматический деплой на боевой сервер при пуше в главную ветку main.
send_massage
Отправка уведомления в телеграм-чат.
## Запуск проекта


