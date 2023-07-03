Описание проекта
Проект по публикации фото котов в интернете.

Технологии
Python 3.9
Django==3.2.3
djangorestframework==3.12.4
Nginx
gunicorn

Установка проекта из репозитория
Клонировать проект с GitHub на сервер: git clone git@github.com:Ваш_аккаунт/<Имя проекта>.git
Находясь в директории с проектом создать и активировать виртуальное окружение python3 -m venv venv source venv/bin/activate
установить зависимости pip install -r requirements.txt
выполнить миграции python manage.py migrate
создать суперюзера python manage.py createsuperuser
отредактировать ALLOWED_HOSTS:
ALLOWED_HOSTS = ['<внешний адрес вашего сервера>', '127.0.0.1', 'localhost' 'ваш_домен']
Заменить стандартное значение 'static' на 'static_backend'.
Указать директорию, куда бэкенд-приложение должно сложить статику.
Собрать статику бэкенд-приложения:
python3 manage.py collectstatic

Запуск frontend проекта на сервере
Находясь в директории с фронтенд-приложением, установить зависимости для него:
npm i
Из директории с фронтенд-приложением выполнить команду:
npm run build
Скопировать статику фронтенд-приложения в директорию по умолчанию:
sudo cp -r путь_к_директории_с_фронтенд-приложением/build/. /var/www/имя_проекта/

Установка и запуск Gunicorn
при активированном виртуальном окружении проекта установить пакет gunicorn pip install gunicorn==20.1.0
запустить Gunicorn:
gunicorn --bind 0.0.0.0:8000 (порт может отличаться) backend.wsgi

Создайте файл конфигурации юнита systemd для Gunicorn в директории
/etc/systemd/system/:
sudo nano /etc/systemd/system/gunicorn_название_проекта.service

Запустить Gunicorn:
sudo systemctl start gunicorn_название_проекта
sudo systemctl enable gunicorn_название_проекта

Установка и настройка Nginx
Запустить Nginx командой:
sudo systemctl start nginx
Обновить настройки Nginx. Для этого отредактировать файл конфигурации веб-сервера
sudo nano /etc/nginx/sites-enabled/default
Перезагрузить конфигурацию Nginx:
sudo systemctl reload nginx

Настройка файрвола ufw
Активировать разрешение принимать запросы только на порты 80, 443 и 22:
sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
Включить файрвол:
sudo ufw enable
Проверить работу файрвола:
sudo ufw status

Получение и настройка SSL-сертификата
Запустить certbot и получить SSL-сертификат:
sudo certbot --nginx и указать домен для сертификата
