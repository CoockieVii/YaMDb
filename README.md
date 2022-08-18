# Проект YaMDb :computer:

## Стэк технологий:
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)

# Описание проекта
Проект **YaMDb** собирает **отзывы (Review)** пользователей на **произведения (Title)** Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список **категорий (Category)** может быть расширен.
Сами произведения в **YaMDb** не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть **произведения**: книги, фильмы или музыка. Например, в категории "Книги" могут быть произведения "Винни Пух и все-все-все" и "Марсианские хроники", а в категории "Музыка" — песня "Давеча" группы "Насекомые" и вторая сюита Баха. Произведению может быть присвоен жанр из списка предустановленных (например, "Сказка", "Рок" или "Артхаус"). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые **отзывы (Review)** и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — **рейтинг** (целое число). На одно произведение пользователь может оставить только один отзыв.

----------
# Алгоритм регистрации пользователей
* Пользователь отправляет POST-запрос с параметром email на `/api/v1/auth/email/`.
* YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
* Пользователь отправляет POST-запрос с параметрами email и confirmation_code на `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен).
* Если письмо не дошло по какой то причине или был утерян token пользователь может выполнить вышеуказанные действия повторно.
----------
# Пользовательские роли

**Аноним** — может просматривать описания произведений, читать отзывы и комментарии.

**Аутентифицированный пользователь (user)** — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.

**Модератор (moderator)** — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.

**Администратор (admin)** — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.

**Администратор Django** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры, имеет доступ к административному интерфейсу Django, может назначать роли пользователям, устанавливать их права.

**Суперюзер Django** — те же права, что и у администратора Django, не зависимо от установленной роли.

----------
# Установка
Системные требования
----------
* Python 3.9+
* Works on Linux, Windows, macOS, BSD

Стек технологий
----------
* Python 3.9
* Django 2.2
* Django Rest Framework
* Pytest
* Simple-JWT
* SQLite3
* Docker-compose

Установка проекта из репозитория (Linux)
----------
1. Клонировать репозиторий и перейти в него в командной строке:
```bash
git clone 'git@github.com:CoockieVii/api_yamdb.git'

cd api_yamdb/infra/
```
2. Запустить проект:
```bash
sudo docker-compose up -d --build 
```
---
3. Запустить миграции, создать суперпользователя и собрать статику (соблюдать последовательность):
```bash
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
----------
4. Доступные нам запросы можем посмотреть в [документации redoc](http://localhost:8000/redoc/).

----------

Авторы:
----------
* **Валитов Ильмир Илсурович**
GitHub - [CoockieVii](https://github.com/CoockieVii)
----------
### MIT License:
#### Copyright (c) 2022 [CoockieVii](https://github.com/CoockieVii)

----------
