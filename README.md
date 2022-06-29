# Окружение для разработки Laravel (Nginx, PHP, MySQL)

### Установка

```console
docker-compose up --build -d

(?) docker-compose exec php composer init
docker-compose exec php composer global require laravel/installer
docker-compose exec php composer create-project laravel/laravel www
```

### Подключение к MySQL

Создаем базу `laravel`:
* Пользователь: root
* Пароль: root
* phpMyAdmin: http://localhost:8081/

Конфигурируем `.env`:
* DB_CONNECTION=mysql
* DB_HOST=db
* DB_PORT=3306
* DB_DATABASE=laravel
* DB_USERNAME=root
* DB_PASSWORD=root

### Основные команды

```console
docker-compose exec php chmod +x /app/www/artisan
docker-compose exec php /app/www/artisan --version
docker-compose exec php /app/www/artisan key:generate

// Новый контроллер
docker-compose exec php /app/www/artisan make:controller MainController

// Очистка кэша (после правки в настройках)
docker-compose exec php /app/www/artisan config:cache

// Создание модели (+ файл миграции)
docker-compose exec php /app/www/artisan make:model ContactModel -m
docker-compose exec php /app/www/artisan migrate

// Миграция
docker-compose exec php /app/www/artisan make:migration user_table
docker-compose exec php /app/www/artisan migrate

// Node.js
docker-compose run --rm npm -v
docker-compose run --rm npm update && npm i
```


### Отправка e-mail'ов

PHP по умолчанию не отправляют настоящих писем при вызове функции ``mail()``.
Все исходящие e-mail'ы перехватываются и пишутся в папку ``app/log/sendmail``.

### Поддержка xDebug для PHP

xDebug уже настроен для использования в контейнерах с PHP7 и PHP8. Для его включения нужно раскомментировать установку модуля в ``config/php*/Dockerfile``.
О настройке PHPStorm для работы с Docker и xDebug 3 можно прочитать в статье [PHP: Настраиваем отладку](https://handynotes.ru/2020/12/phpstorm-php-8-docker-xdebug-3.html).