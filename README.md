![workflow](https://github.com/SERG40/foodgram-project-react/actions/workflows/main.yml/badge.svg)

##  Проект Foodgram

**Foodgram** - приложение в котором пользователи могут публиковать рецепты, добавлять чужие рецепты в избранное и подписываться на публикации других авторов. Сервис «Foodgram» позволяет пользователям создавать список продуктов, которые нужно купить для приготовления выбранных блюд.

Проект доступен по адресу (http://51.250.31.241/) <br>

## ⚙ Используемые технологии:

▪ **Python**<br>
▪ **Django**<br>
▪ **DRF**<br>
▪ **Docker**<br>
▪ **Gunicorn**<br>
▪ **NGINX**<br>
▪ **PostgreSQL**<br>
▪ **Yandex Cloud**<br>
▪ **CI/CD**<br>

## 📃 Как развернуть проект на сервере:

Клонировать репозиторий:
```
git@github.com:SERG40/foodgram-project-react.git
```

Установить на сервере Docker, Docker Compose:

```
sudo apt install curl                                   # установка утилиты для скачивания файлов
curl -fsSL https://get.docker.com -o get-docker.sh      # скачать скрипт для установки
sh get-docker.sh                                        # запуск скрипта
sudo apt-get install docker-compose-plugin              # последняя версия docker compose
```

Скопировать на сервер файлы docker-compose.yml, nginx.conf из папки infra (команды выполнять находясь в папке infra):

```
scp docker-compose.yml nginx.conf <username>@<IP>:/home/<username>/   # username - имя пользователя на сервере
                                                                      # IP - публичный IP сервера
```
Создать файл .env и заполнить своими данными:
```
touch .env
nano .env
```
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY=1234567890
```

Создать и запустить контейнеры Docker, выполнить команду на сервере

sudo docker compose up -d
```

После успешной сборки выполнить миграции:
```
sudo docker compose exec backend python manage.py makemigrations
sudo docker compose exec backend python manage.py migrate
```

Создать суперпользователя:
```
sudo docker compose exec backend python manage.py createsuperuser
```

Собрать статику:
```
sudo docker compose exec backend python manage.py collectstatic --noinput
```

Наполнить базу данных:
```
sudo docker compose exec backend python manage.py loaddata ingredients.json
```



Для остановки контейнеров Docker:
```
sudo docker compose down -v      # с их удалением
sudo docker compose stop         # без удаления
```

Для работы с GitHub Actions необходимо в репозитории в разделе Secrets > Actions создать переменные окружения:
```
SECRET_KEY              # секретный ключ Django проекта
DOCKER_PASSWORD         # пароль от Docker Hub
DOCKER_USERNAME         # логин Docker Hub
HOST                    # публичный IP сервера
USER                    # имя пользователя на сервере
PASSPHRASE              # *если ssh-ключ защищен паролем
SSH_KEY                 # приватный ssh-ключ
TELEGRAM_TO             # ID телеграм-аккаунта для посылки сообщения
TELEGRAM_TOKEN          # токен бота, посылающего сообщение
DB_ENGINE               # django.db.backends.postgresql
DB_NAME                 # postgres
POSTGRES_USER           # postgres
POSTGRES_PASSWORD       # postgres
DB_HOST                 # db
DB_PORT                 # 5432 (порт по умолчанию)
```

### После каждого обновления репозитория (push в ветку master) будет происходить:

1. Проверка кода на соответствие стандарту PEP8 (с помощью пакета flake8)
2. Сборка и доставка докер-образов frontend и backend на Docker Hub
3. Разворачивание проекта на удаленном сервере
4. Отправка сообщения в Telegram в случае успеха

### Запуск проекта на локальной машине:

Клонировать репозиторий:
```
git@github.com:SERG40/foodgram-project-react.git
```

В директории infra файл example.env переименовать в .env и заполнить своими данными:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY=1234567890
```

Создать и запустить контейнеры Docker, как указано выше.



## Автор Кастов Сергей
