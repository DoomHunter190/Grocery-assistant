### Опиание проекта.
«Продуктовый помощник». Это онлайн-сервис и API для него. На этом сервисе пользователи могут публиковать рецепты, подписываться на публикации других пользователей, добавлять понравившиеся рецепты в список «Избранное», формировать список покупок для приготовления рецептов.

## Инструкции по установке

***- Установите и активируйте виртуальное окружение:***
```
python -3.9 -m venv venv
source venv/Scripts/activate
```

***- Установите зависимости из файла requirements.txt:***
```
pip install -r requirements.txt
```

***- Примените миграции:***
```
python manage.py migrate
```

***- В файле для локального запуска изменить параметр DEBUG:***
```
DEBUG = True # os.getenv('DEBUG', default=False)
```

***- В папке backend с файлом manage.py выполните команду для запуска backend:***
```
python manage.py runserver
```

***- Локально backend доступен по адресу:***

```
http://127.0.0.1/api/
```

### Подготовка к запуску проекта на удаленном сервере

Cоздать и заполнить .env файл в директории infra
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=example
POSTGRES_USER=example
POSTGRES_PASSWORD=example
DB_HOST=example
DB_PORT=5432
TOKEN=example
ALLOWED_HOSTS=*
```

### Собираем контейнерыы:
Из папки infra/ разверните контейнеры при помощи docker-compose:
```
docker-compose up -d --build
```

Выполните миграции:
```
docker compose exec backend python manage.py migrate
```

Создайте суперпользователя:
```
docker compose exec backend python manage.py createsuperuser
```

Соберите статику:
```
docker compose exec backend python manage.py collectstatic --no-input
```
Наполните базу данных ингредиентами и тегами. Выполняйте команду:
```
docker compose exec backend python manage.py load_data
```

Чтобы остановить проект:
```
docker-compose down
```

### Примеры запросов:

**`GET` | Список рецептов: `http://127.0.0.1:8000/api/recipes/`**

Response:
```
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "tags": [
                {
                    "id": 1,
                    "name": "test",
                    "color": "#FFFFFF",
                    "slug": "test"
                }
            ],
            "author": {
                "email": "max@mail.ru",
                "id": 2,
                "username": "max",
                "first_name": "example",
                "last_name": "example",
                "is_subscribed": false
            },
            "ingredients": [
                {
                    "id": 3,
                    "name": "ингридиент 3",
                    "measurement_unit": "л",
                    "amount": 2
                },
                {
                    "id": 2,
                    "name": "ингридиент 2",
                    "measurement_unit": "мл",
                    "amount": 4
                },
                {
                    "id": 1,
                    "name": "ингридиент 1",
                    "measurement_unit": "шт",
                    "amount": 2
                }
            ],
            "is_favorited": false,
            "is_in_shopping_cart": false,
            "name": "название",
            "image": "http://127.0.0.1:8000/media/recipes/image/images.jpg",
            "text": "описание",
            "cooking_time": 25
        }
    ]
}
```

**`POST` | Создание рецепта: `http://127.0.0.1:8000/api/recipes/`**
Request:
```
{
  "ingredients": [
    {
      "id": 213,
      "amount": 10
    }
  ],
  "tags": [
    1,
    2
  ],
  "image": "",
  "name": "string",
  "text": "string",
  "cooking_time": 1
}
```
Response:
```
{
  "id": 0,
  "tags": [
    {
      "id": 0,
      "name": "Завтрак",
      "color": "#E26C2D",
      "slug": "breakfast"
    }
  ],
  "author": {
    "email": "user@example.com",
    "id": 0,
    "username": "string",
    "first_name": "example",
    "last_name": "example",
    "is_subscribed": false
  },
  "ingredients": [
    {
      "id": 0,
      "name": "Картофель отварной",
      "measurement_unit": "г",
      "amount": 1
    }
  ],
  "is_favorited": true,
  "is_in_shopping_cart": true,
  "name": "string",
  "image": "",
  "text": "string",
  "cooking_time": 1
}
```
Author of the project | My mail
------------- | -------------
[Doomhunter190](https://github.com/DoomHunter190) | <small>[maximportnov9999@gmail.com](maximportnov9999@gmail.com)
