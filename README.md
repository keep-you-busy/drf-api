# Описание
Yatube API - это проектная работа Django REST: здесь применены **вьюсеты**, а аутентификация проходит через **JWT**.

# Установка
Для запуска проекта:
1. Клонируйте репозиторий
```bash
git clone https://github.com/your_username_/Project-Name.git
```
2. Создайте окружение
```bash
python3 -m venv venv
```
3. Активируйте окружение
```bash
source venv/bin/activate
```
4. Установите все необходимые зависимости
```bash
pip install -r requirements.txt
```
5. Выполните все миграции
```bash
python3 yatube_api/manage.py makemigrations
```
```bash
python3 yatube_api/manage.py migrate
```
6. Запустите сервер
```bash
python3 yatube_api/manage.py runserver
```

**Теперь по адресу http://127.0.0.1:8000/redoc/ вы можете воспользоваться документацией**
# Примеры
##  <span style="color:green">**GET**</span> Получение публикаций
Получить список всех публикаций. При указании параметров limit и offset выдача будет работать с пагинацией.

<span style="color:green">**GET**</span> */api/v1/posts/*

<span style="color:green">**200**</span> - удачное выполнение запроса
```json
{
  "count": 123,
  "next": "http://api.example.org/accounts/?offset=400&limit=100",
  "previous": "http://api.example.org/accounts/?offset=200&limit=100",
  "results": [
    {
      "id": 0,
      "author": "string",
      "text": "string",
      "pub_date": "2021-10-14T20:41:29.648Z",
      "image": "string",
      "group": 0
    }
  ]
}
```

##  <span style="color:blue">**POST**</span> Создание публикации
Добавление новой публикации в коллекцию публикаций. Анонимные запросы запрещены.

<span style="color:blue">**POST**</span> */api/v1/posts/*

<span style="color:red">**401**</span> - Запрос от имени анонимного пользователя
```json
{
  "detail": "Учетные данные не были предоставлены."
}
```

##  <span style="color:purple">**PUT**</span> Создание публикации
Обновление публикации по id. Обновить публикацию может только автор публикации. Анонимные запросы запрещены.

<span style="color:purple">**PUT**</span> */api/v1/posts/{id}/*

<span style="color:red">**400**</span> - Отсутсвует обязательное поле в теле запроса
```json
{
  "text": [
    "Обязательное поле."
  ]
}
```
##  <span style="color:orange">**PATCH**</span> Частичное обновление публикации
Частичное обновление публикации по id. Обновить публикацию может только автор публикации. Анонимные запросы запрещены.

<span style="color:orange">**PATCH**</span> */api/v1/posts/{id}/*

<span style="color:red">**404**</span> - Попытка изменения несуществующей публикации
```json
{
  "detail": "Страница не найдена."
}
```
##  <span style="color:red">**DELETE**</span> Удаление публикации
Удаление публикации по id. Удалить публикацию может только автор публикации. Анонимные запросы запрещены.

<span style="color:red">**DELETE**</span> */api/v1/posts/{id}/*

<span style="color:red">**403**</span> - Попытка изменения чужого контента
```json
{
  "detail": "У вас недостаточно прав для выполнения данного действия."
}
```

