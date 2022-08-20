# Проект YaMDb :computer:

----------

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

Проект **Yamdb_infra** собирает отзывы пользователей на произведения.
Произведения
делятся на категории: "Книги", "Фильмы", "Музыка". Список категорий может быть
расширен.
Сами произведения в **YaMDb** не хранятся, здесь нельзя посмотреть фильм или
послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в
категории "Книги" могут быть произведения "Винни Пух и все-все-все" и "
Марсианские хроники", а в категории "Музыка" — песня "Давеча" группы "
Насекомые" и вторая сюита Баха. Произведению может быть присвоен жанр из списка
предустановленных (например, "Сказка", "Рок" или "Артхаус"). Новые жанры может
создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые
отзывы и ставят произведению оценку в диапазоне от одного до
десяти (целое число); из пользовательских оценок формируется усреднённая оценка
произведения — рейтинг (целое число). На одно произведение пользователь
может оставить только один отзыв.

----------

## Алгоритм регистрации пользователей:

* Пользователь отправляет POST-запрос с параметром email
  на `/api/v1/auth/email/`.
* YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес
  email.
* Пользователь отправляет POST-запрос с параметрами email и confirmation_code
  на `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен).
* Если письмо не дошло по какой то причине или был утерян token пользователь
  может выполнить вышеуказанные действия повторно.

## Пользовательские роли:

* **Аноним** — может просматривать описания произведений, читать отзывы и
  комментарии.

* **Аутентифицированный пользователь (user)** — может, как и Аноним, читать
  всё,
  дополнительно он может публиковать отзывы и ставить оценку произведениям (
  фильмам/книгам/песенкам), может комментировать чужие отзывы; может
  редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по
  умолчанию каждому новому пользователю.

* **Модератор (moderator)** — те же права, что и у Аутентифицированного
  пользователя плюс право удалять любые отзывы и комментарии.

* **Администратор (admin)** — полные права на управление проектом и всем его
  содержимым. Может создавать и удалять произведения, категории и жанры. Может
  назначать роли пользователям.

* **Администратор Django** — полные права на управление всем контентом проекта.
  Может создавать и удалять произведения, категории и жанры, имеет доступ к
  административному интерфейсу Django, может назначать роли пользователям,
  устанавливать их права.

* **Суперюзер Django** — те же права, что и у администратора Django, не
  зависимо
  от установленной роли.

----------

## Установка проекта*

###### *скопируйте содержимое поля снизу и запустите через командную строку.

```bash
# - Скачиваем проект.
git clone 'git@github.com:cookievii/Yamdb_infra.git'
# - Переходим в папку "infra".
cd infra/
# - Создаем файл с секретами(Шаблон наполнения показан ниже).
touch .env
# - Запускаем docker-compose.
docker-compose up -d --build
# - Выполняем миграции БД.
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate
# - Создаем суперпользователя:
docker-compose exec web python manage.py createsuperuser
# - Собераем статику:
docker-compose exec web python manage.py collectstatic --no-input
```

----------

## Документация с примерами запросов и ответов*

###### *Доступна после запуска проекта

Документация для API: [доступна по ссылке](http://localhost:8000/redoc/)

----------

## Авторы:

* **Валитов Ильмир Илсурович**
  GitHub - [cookievii](https://github.com/cookievii)

----------

## MIT License:

#### Copyright (c) 2022 [cookievii](https://github.com/cookievii)