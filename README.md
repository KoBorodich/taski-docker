Kittygram — финальный проект по Docker и CI/CD

Проект Kittygram — это учебное приложение для загрузки и просмотра фотографий котиков.
В финальном спринте проект был полностью контейнеризован и настроен на автоматический деплой на удалённый сервер с помощью GitHub Actions.

Технологии

Python 3.9 / Django
PostgreSQL (в Docker)
Nginx (в связке с Docker gateway)
Docker / docker-compose
GitHub Actions (CI/CD)
Frontend — React (в отдельном контейнере)

Используемые Docker-образы

При сборке в GitHub Actions создаются и загружаются на Docker Hub:
konstantinbor/kittygram_backend
konstantinbor/kittygram_frontend
konstantinbor/kittygram_gateway
postgres:13 (официальный)
Контейнеры в docker-compose.production.yml
db — PostgreSQL
backend — Django + gunicorn
frontend — статический React-бандл
gateway — Nginx, который раздаёт статику и проксирует запросы на backend

Volumes

pg_data — данные БД
static — статика Django + фронта
media — пользовательские файлы

CI/CD

При пуше в ветку main происходит:
Проверка кода (PEP8)
Запуск тестов (frontend + backend)
Сборка Docker-образов
Публикация образов на Docker Hub
Подключение к серверу по SSH
docker compose pull + docker compose up -d
Выполнение миграций
Сборка статики
Отправка уведомления в Telegram об успешном деплое

Продакшен-домен

Kittygram доступен по адресу:
https://homeprojectko.duckdns.org

Автор

Константин Бородич
GitHub: KoBorodich