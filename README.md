Docker + Django + React

Full-stack pet-проект с использованием Django, React, PostgreSQL, Nginx и Docker Compose.
Проект собран для демонстрации навыков контейнеризации, разделения сервисов и настройки взаимодействия frontend - backend.

Используемый стек: Backend - Django; Frontend - React (production build); Database - PostgreSQL; Web server/proxy - Nginx; Оркестрация - Docker Compose.

Архитектура проекта: Проект состоит из нескольких изолированных контейнеров.
Django - backend API; React - frontend, собранный в production и отдаваемый через Nginx; PostgreSQL - БД; Nginx - Отдает статические файлы frontend и проксирует все запросы /api/* в backend.
Все сервисы взаимодействуют через Docker-сеть, без прямого доступа к базе данных извне.

Структура проекта:

<img width="316" height="467" alt="image" src="https://github.com/user-attachments/assets/5bb9f56c-9903-4552-ac86-211947ef3ff2" />

Проект полностью поднимается одной командой:
docker compose up -d

Применить миграции базы данных:
docker compose exec backend python manage.py migrate

Доступ:
http://localhost:8080

Особенности и best practices:
Frontend и PostgreSQL изолированы и подключены к backend через Docker-сеть; React собирается в production build, Node.js не используется в runtime; Nginx выполняет роль web-сервера для frontend и reverse proxy для backend API; Backend и база данных не доступны напрямую извне.
Четкое разделение сервисов: frontend / backend / database

Исходный код проекта был взят из учебного курса по Docker (EPAM) и доработан: Настроена контейнеризация; Исправлены сетевые взаимодействия; Добавлен Nginx proxy; Реализована production-сборка frontend.
