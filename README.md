# Docker-окружение для Symfony

Базовый инфраструктурный шаблон для будущего Symfony-приложения. Поднимаются сервисы: php-fpm (app), nginx, mysql, redis, memcached.

## Стек технологий
- PHP 8.x + Symfony (проект ставится в `app/`)
- MySQL 8
- Redis и Memcached
- Nginx
- Docker, Docker Compose
- Webpack (через Symfony/Webpack Encore позже)
- Composer
- Ориентировано на деплой на Linux/Ubuntu-сервер

## Запуск инфраструктуры
Требуются Docker и Docker Compose.

1. Клонировать репозиторий и перейти в каталог проекта.
2. Запустить окружение: `docker compose up -d` (или `docker-compose up -d`).
3. Проверить работу контейнеров: `docker compose ps`.

## Установка нового Symfony-проекта внутрь контейнера
1. Зайти в PHP-контейнер: `docker compose exec app bash`.
2. Перейти в `/var/www/app` (папка смонтирована из хоста).
3. Установить Symfony одним из способов:
   - `composer create-project symfony/skeleton .`
   - или `symfony new . --webapp` (если symfony-cli доступен).
4. После установки убедиться, что в `app/` появились стандартные каталоги Symfony (`bin/`, `config/`, `public/`, `src/` и т.д.).
5. Настроить `DATABASE_URL` на подключение к `mysql` с базой `symfony`, пользователем `symfony`, паролем `symfony`.
6. Выполнить проверки: `php bin/console about`, при необходимости `php bin/console doctrine:database:create`.
7. Открыть http://localhost:8080 и убедиться, что отображается дефолтная страница Symfony.

## Redis и Memcached
Сервисы Redis и Memcached уже доступны внутри Docker-сети по хостам `redis` и `memcached` и могут использоваться для кэша или сессий после настройки в Symfony.
