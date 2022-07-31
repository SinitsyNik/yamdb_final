![example workflow](https://github.com/SinitsyNik/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# yamdb_final

## Описание:
Это API проекта yamdb, позволяющего хранить отзывы пользователей на различные произведения.

## Как запустить:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:SinitsyNik/yamdb_final.git
```

```
cd infra_sp2
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv venv
```

```
source venv/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Перейти в папку с docker-compose:

```
cd infra
```

Затем развернуть контейнеры:

```
docker-compose up -d --build  
```

Выполнить миграции::

```
docker-compose exec web python manage.py migrate
```

Создайть суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

Создайть дамп базы данных:

```
docker-compose exec web python manage.py dumpdata > fixtures.json
```

Подключить статику:

```
docker-compose exec web python manage.py collectstatic --no-input 
```

Остановить контейнеры:

```
docker-compose down -v 
```

## Дополнительно:
В директории infra создать фаил .env и заполнить
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password # укажите свой пароль
DB_HOST=db
DB_PORT=5432
```

## Технологии:

- python
- django
- django rest framework
- django-filter
- docker
- gunicorn
- nginx
- postgreSQL

## Список доступных команд:
Подробное описание всех эндпоинтов можно найти по адресу http://51.250.106.212/redoc/ после запуска проекта на локальном сервере

### Примеры

- Получение JWT-токена:

Запрос:
```
POST http://51.250.106.212/api/v1/auth/token/
{
  "username": "string",
  "confirmation_code": "string"
}
```
Ответ:
```
{
  "token": "string"
}
```


- Получение списка всех категорий:

Запрос:
```
GET http://51.250.106.212/api/v1/categories/
```
Ответ:
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
```


- Добавление жанра:

Запрос:
```
POST http://51.250.106.212/api/v1/genres/
{
  "name": "string",
  "slug": "string"
}
```


- Получение списка всех комментариев к отзыву:

Запрос:
```
POST http://51.250.106.212/api/v1/titles/{title_id}/reviews/{review_id}/comments/
{
  "text": "string"
}
```
Ответ:
```
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2019-08-24T14:15:22Z"
}
```


- Получение списка всех пользователей(Доступно аутентифицированным пользователям):

Запрос:
```
GET http://51.250.106.212/api/v1/users/
```
Ответ:
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "username": "string",
        "email": "user@example.com",
        "first_name": "string",
        "last_name": "string",
        "bio": "string",
        "role": "user"
      }
    ]
  }
]
```

## Автор:

### Никита Синицын

