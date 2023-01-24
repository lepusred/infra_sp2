### Описание:

Проект **api_yamdb** это бекэнд для сайта-агрегатора рецензий **YaMDb**, на котором вы можете посмотреть рейтинг интересующего вас произведения, написать о нем отзыв и поставить оценку, также вы можете комментировать чужие отзывы. 

 **api_yamdb** дает возможность передавать данные с помощью **REST API** интерфейса, доступные действия:

- регистрация пользователя

- получение или обновление токена

- получение полного списка произведений

- просмотр уже имеющихся отзывов или добавление своего

- добавление комментария к другим отзывам

  и еще много всего.

  Полный список доступных эндпоинтов можно посмотреть здесь http://127.0.0.1:8000/redoc/, эта ссылка будет доступна после того как вы запустите проект, ниже описание того как это сделать. 

  *Замечание:* Для работы **redoc** необходимо в *settings.py* установить *DEBUG=True*

### Как запустить проект: 

В консоли bash:

Клонируйте репозиторий в командной строке в нужную вам папку:

```
git clone https://github.com/lepusred/infra_sp2.git
```

Перейдите в папку infra_sp2:

```
cd /infra_sp2
```

Cоберите контейнеры и запустите их внутри этой папки:

```
docker-compose up -d --build
```

Выполните миграции:

```
docker-compose exec web python manage.py migrate
```

Создайте суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

Подгрузите статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Теперь можно посмотреть список эндпоинов по ссылке

 http://127.0.0.1:8000/redoc/



### Примеры запросов:

#### Получить токен

```
POST http://127.0.0.1:8000/api/v1/auth/token/
Content-Type: application/json

{
    "username": "alena",
    "confirmation_code": "64u-188bc42c1126464cff29"
}
```

#### Добавить произведение( доступно только администраторам сайта)

```
POST http://127.0.0.1:8000/api/v1/titles/
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjY1NDk1NjUxLCJpYXQiOjE2NjU0MDkyNTEsImp0aSI6IjkzMDI4Y2U2Yzc4MzQ4ZmRiMGQzYjAzMzdhOGU1NDhkIiwidXNlcl9pZCI6Mn0.Csq5sVXLhJTbYsZNdU7g5r2bRhsLXwtKchNUAmyi6uE

{
"name": "song",
"year": 2020,
"genre": ["comedy","dram"],
"category": "books"
}
```

#### Посмотреть список всех произведений

```
http://127.0.0.1:8000/api/v1/titles/ 
```
