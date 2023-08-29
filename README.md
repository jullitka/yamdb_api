# Проект YaMDb API

## Возможности:
- Возможность оставлять отзывы на произведения (книги, фильмы, музыка) и ставить оценку от 1 до 10.
- Регистрация новых пользователей 
- JWT-аунтефикация
- Получения списков (категории, жанры, произведения, отзывы, комментарии), а также данных о конктреных объектах (произведения, отзывы, комментарии)

## Стек технологий:
[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)

## Запуск проекта
- Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/jullitka/yamdb_api.git
cd api_yamdb
```

- Cоздать и активировать виртуальное окружение:

```
python -m venv venv
```

* Если у вас Linux/macOS

    ```
    source env/bin/activate
    ```

* Если у вас Windows

    ```
    source venv/Scripts/activate
    ```

- Установить зависимости из файла requirements.txt:

```
python -m pip install --upgrade pip
pip install -r requirements.txt
```

- Выполнить миграции:

```
python manage.py migrate
```

- Запустить проект:

```
python manage.py runserver
```

Документация к API доступна после запуска проекта по ссылке: http://127.0.0.1/redoc/

## Примеры запросов API
- Базовый url
```
api/v1
```
Добавляйте базовый url перед конечными точками.

- Доступные методы: GET, POST, PATCH, DELETE

- Данные о категориях, жанрах, произведениях, отзывах и комментарих к ним доступны любому пользователю.

- Получить данные о пользователях, изменять и удалять их может только администратор.

- Получать и изменять данные своей учетной записи может также любой зарегистрированный пользователь.

- Добавлять отзывы и комментарии может только авторизированный пользователь.

- Добавлять и удалять категории, жанры и произведения может только администратор.

- Удалять и редактировать публикации и комментарии может только их автор, администратор или модератор.


### Регистрация нового пользователей:

Выбирайте метод POST для регистрации.
```
/auth/signup/
```
Данные, передаваемые в теле запроса:
```
{
"email": "user@example.com",
"username": "имя пользователя"
}
```
После удачного выполнения запроса на вае email придет письмо с кодом подтверждения (confirmation_code).
Введите его в запросе для получения токена. 

### Получение JWT-токена:

Выбирайте метод POST для получения токена.
```
/auth/token/
```
Данные, передаваемые в теле запроса:
```
{
"username": "имя пользователя",
"confirmation_code": "код из письма"
}
```

### Выбирайте метод GET для выполнения следующих запросов к конечным точкам:
#### Получение списка категорий:
```
/categories/
```
#### Получение списка жанров:
```
/genres/
```
#### Получение списка произведений:
```
/titles/
```
#### Получение информации о произведении:
```
/titles/<id_произведения>/
```
#### Получение списка всех отзывов к произведению:
```
/titles/<id_произведения>/reviews/
```
#### Получение отзыва к произведению по id:
```
/titles/<id_произведения>/reviews/<id_отзыва>
```
#### Получение списка всех комментариев к отзыву:
```
/titles/<id_произведения>/reviews/<id_отзыва>/comments/
```
#### Получение комментария к отзыву по id:
```
/titles/<id_произведения>/reviews/<id_отзыва>/comments/<id_комментария>
```
#### Получение списка всех пользователей (доступно только администратору):
```
/users/
```
#### Получение данных пользователя по username (доступно только администратору):
```
/users/<username>/
```
#### Получение данных своей учетной записи:
```
/users/me/
```

### Выбирайте метод POST для выполнения следующих запросов к конечным точкам:
#### Добавление новой категории (доступно только администратору):
```
/categories/
```
Данные, передаваемые в теле запроса:

```
{
"name": "название категории",
"slug": "уникальный slug"
}
```

#### Добавление нового жанра (доступно только администратору):
```
/genres/
```
Данные, передаваемые в теле запроса:

```
{
"name": "название жанра",
"slug": "уникальный slug"
}
```

#### Добавление нового произведения(доступно только администратору):
```
/titles/
```
Данные, передаваемые в теле запроса:

```
{
"name": "название произведения",
"year": год выпуска (число),
"description": "описание",
"genre": [
"slug жанра"
],
"category": "slug категории"
}
```

#### Добавление нового отзыва к произведению:
```
/titles/<id_произвеления>/reviews/
```
Данные, передаваемые в теле запроса:

```
{
"text": "текст отзыва",
"score": оценка (число от 1 до 10)
}
```
#### Добавление комментария к отзыву:
```
/titles/<id_произведения>/reviews/<id_отзыва>/comments/
```
Данные, передаваемые в теле запроса:
```
{
"text": "текст комментари"
}
```
### Выбирайте метод DELETE для выполнения следующих запросов к конечным точкам:
#### Удаление категории (доступно только администратору):
```
/categories/<slug>/
```

#### Удаление жанра (доступно только администратору):
```
/genres/<slug>/
```
#### Удаление произведения (доступно только администратору):
```
/titles/<id_произведения>/
```
#### Удаление отзыва (доступно авторизованному пользователю, модератору и администратору):
```
/titles/<id_произведения>/reviews/<id_отзыва>
```
#### Удаление комментария к отыву (доступно авторизованному пользователю, модератору и администратору):
```
/titles/<id_произведения>/reviews/<id_отзыва>/comments/<id_комментария>/
```
#### Удаление пользователя (доступно только администратору):
```
/users/<username>/
```
### Выбирайте метод PATCH для выполнения следующих запросов к конечным точкам:

#### Частичное обновление информации о произведении (доступно только администратору):
```
/titles/
```
Данные, передаваемые в теле запроса:

```
{
"name": "название произведения",
"year": год выпуска (число),
"description": "описание",
"genre": [
"slug жанра"
],
"category": "slug категории"
}
```
#### Частичное обновление отзыва к произведению (доступно автору, модератору и администратору):
```
/titles/<id_произведения>/reviews/<id_отзыва>
```
Данные, передаваемые в теле запроса:

```
{
"text": "текст отзыва",
"score": оценка (число от 1 до 10)
}
```
#### Частичное обновление комментария к отзыву (доступно автору, модератору и администратору):
```
/titles/<id_произведения>/reviews/<id_отзыва>/comments/<id_комментария>
```
Данные, передаваемые в теле запроса:
```
{
"text": "текст комментари"
}
```

#### Изменение данных пользователя (доступно только администратору):
```
/users/<username>/
```
Данные, передаваемые в теле запроса:
```
{
"username": "имя пользователя",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string",
"role": "user"
}
```

#### Изменение данных своей учетной записи:
```
/users/me/
```
Данные, передаваемые в теле запроса:
```
{
"username": "имя пользователя",
"email": "user@example.com",
"first_name": "string",
"last_name": "string",
"bio": "string"
}
```
## Авторы

[Юлия Пашкова](https://github.com/Jullitka)

[Никита Федоров](https://github.com/oupsfed)

