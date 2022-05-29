![example workflow](https://github.com/Sonanted/yamdb_final/actions/workflows/yamdb_workflow/badge.svg)
# api_yamdb
## Проект YaMDb собирает отзывы пользователей на различные произведения

Проект предоставляет API в виде REST-сервиса для YaMDb.

## Возможности

- Создавать и редактировать отзывы на произведения, оценивать их
- Комментировать отзывы
- Аутентификация через JWT

## Технологии

Проект использует:
- [Django](https://www.djangoproject.com/) -  свободный фреймворк для веб-приложений на языке Python
- [Django Rest Framework](https://www.django-rest-framework.org/) - гибкий и мощный фреймворк для построения Web API
- [Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io) - плагин JSON Web Token аутентификации для Django REST Framework
- [Docker](https://www.docker.com/) - упаковка приложений в контейнеры

## Как запустить проект

Клонировать репозиторий и перейти в него в командной строке:
```bash
git clone https://github.com/mshabanov/api_yamdb.git
cd api_yamdb
```
Перейти в папку infra, откуда упаковать и запустить приложение:
```bash
cd infra
docker-compose up -d --build
```
После запуска приложения выполнить миграции:
```bash
docker-compose exec web python manage.py migrate
```
Далее создать суперпользователя :
```bash
docker-compose exec web python manage.py createsuperuser
```
И собрать всю статику приложения:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```
После этого приложение станет доступным по адресу http://localhost/
Зайти под админкой и добавить фикстур можно по адресу http://localhost/admin/

При необходимости можно сделать дамп базы данных:
```
docker-compose exec web python manage.py dumpdata > fixtures.json
```


## Шаблон наполнения файла .env
В проект включены переменные окружения:
|Ключ                    |Значение                              |
-------------------------|--------------------------------------|
|DB_ENGINE               | СУБД, используемая в приложении      |
|DB_NAME                 | имя базы данных                      |
|POSTGRES_USER           | логин для входа в базу данных        |
|POSTGRES_PASSWORD       | пароль для входа в базу данных       |
|DB_HOST                 | название контейнера базы данных      |
|DB_PORT                 | порт для подключения к базе данных   |


## Ресурсы API YaMDb

|Ресурс                             | Описание                      |
------------------------------------|-------------------------------|
|/api/v1/auth/                      | аутентификация                |
|/api/v1/users/                     | пользователи                  |
|/api/v1/titles/                    | произведения                  |
|/api/v1/categories/                | категории произведений        |
|/api/v1/genres/                    | жанры произведений            |
|/api/v1/reviews/                   | отзывы на произведения        |
|/api/v1/comments/                  | комментарии к отзывам         |


## Команда разработки 

| Имя            | Роль                                                       | Контакты                     |
-----------------|------------------------------------------------------------|----------------------------- |
|Михаил Шабанов  |Тимлид, пользователи, система регистрации и аутентификации  | https://github.com/mshabanov |
|Евгений Кириллов|Categories, Genres, Titles                                  | https://github.com/n0n6m3    |
|Андрей Никоненко|Review, Comments, рейтинги, права доступа                   | https://github.com/Sonanted  |

## License

MIT