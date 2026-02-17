<!--Версия README не является действующей. При выполнении проекта README будет полностью переделан.-->
# TaskFlow / ProjectMaster

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![Flask 3.0+](https://img.shields.io/badge/Flask-3.0+-lightgrey.svg)](https://flask.palletsprojects.com/)

**Умный планировщик задач** для эффективного управления проектами, дедлайнами и командной работой. Проект находится в стадии активной разработки.

Наша цель — создать интуитивный инструмент, объединяющий в себе простоту to-do листа, гибкость канбан-доски и наглядность календаря.

## Оглавление

- [О проекте](#о-проекте)
- [Ключевые возможности (Roadmap)](#ключевые-возможности-roadmap)
- [Технологический стек](#технологический-стек)
- [Начало работы](#начало-работы)
- [Структура базы данных (MVP)](#структура-базы-данных-mvp)
- [API Эндпоинты (план)](#api-эндпоинты-план)
- [Планы по развитию](#планы-по-развитию)
- [Как внести вклад](#как-внести-вклад)
- [Лицензия](#лицензия)

## О проекте

**Суть проекта:** Управление задачами с использованием продвинутой системы фильтрации (теги, проекты, приоритеты) и визуализации (канбан, календарь).

В отличие от стандартных планировщиков, мы делаем упор на:
- **Гибкую организацию задач** через проекты и теги.
- **Визуальное управление статусами** через drag-and-drop (как в Trello/Notion).
- **Встроенный календарь** для планирования дедлайнов.

## Ключевые возможности (Roadmap)

Проект разбит на несколько этапов разработки:

### Этап 1: Ядро (MVP)
- [ ] **Пользователи**: Система аутентификации JWT (регистрация/вход).
- [ ] **Проекты**: Создание проектов для группировки задач.
- [ ] **Задачи**: CRUD для задач (название, описание, дедлайн, статус).
- [ ] **Теги**: Возможность создавать теги и прикреплять их к задачам для гибкой фильтрации.

### Этап 2: Визуализация и Управление
- [ ] **Канбан-доска**: Отображение задач в колонках по статусу.
- [ ] **Drag-and-Drop**: Перемещение задач между колонками для смены статуса.
- [ ] **Календарь**: Отображение задач с дедлайнами на календаре (неделя/месяц).
- [ ] **Приоритеты**: Добавление уровней приоритета (Низкий, Средний, Высокий, Критичный).

### Этап 3: Умные функции и Коллаборация
- [ ] **Напоминания**: Email и/или уведомления в браузере о приближающихся дедлайнах.
- [ ] **Поиск и фильтры**: Быстрый поиск по задачам и фильтрация по тегам/проектам/статусу.
- [ ] **Совместная работа**:
  - [ ] Приглашение пользователей в проект.
  - [ ] Назначение исполнителей на задачи.
  - [ ] Система комментариев к задачам.

## Технологический стек

### Бэкенд
- **Язык**: Python 3.12+
- **Фреймворк**: Flask 3.0+ (RESTful API)
- **База данных**: SQLite (для разработки) / PostgreSQL (для продакшена)
- **ORM**: SQLAlchemy (с Flask-SQLAlchemy)
- **Миграции**: Flask-Migrate (Alembic)
- **Аутентификация**: Flask-JWT-Extended
- **Сериализация**: Marshmallow (с Flask-Marshmallow)
- **Валидация**: Marshmallow-schemas

### Фронтенд
- **Язык**: TypeScript
- **Фреймворк**: React (или Vue.js на выбор)
- **Стейт-менеджмент**: Redux Toolkit / Pinia
- **Стили**: Tailwind CSS
- **Drag-and-Drop**: dnd-kit
- **Календарь**: FullCalendar

### Инфраструктура
- **Контейнеризация**: Docker, Docker Compose (для продакшена с PostgreSQL)
- **Веб-сервер**: Nginx + Gunicorn
- **CI/CD**: GitHub Actions

## Начало работы

### Предварительные требования
- Python 3.12+
- Node.js 18+ и npm
- Git

### Установка и запуск (Режим разработки)

1. **Клонируйте репозиторий**
   ```bash
   git clone https://github.com/yourusername/task-manager.git
   cd task-manager
   ```

2. **Настройка бэкенда (Flask)**
   ```bash
   # Перейдите в папку бэкенда
   cd backend

   # Создайте виртуальное окружение
   python -m venv venv

   # Активируйте виртуальное окружение
   # Для Linux/Mac:
   source venv/bin/activate
   # Для Windows:
   # venv\Scripts\activate

   # Установите зависимости
   pip install -r requirements.txt

   # Настройте переменные окружения
   # Создайте файл .env на основе .env.example
   cp .env.example .env
   # Отредактируйте .env, установите SECRET_KEY и другие параметры

   # Инициализируйте базу данных (SQLite)
   # Команда создаст файл базы данных instance/tasks.db и все таблицы
   flask shell
   >>> from app import db
   >>> db.create_all()
   >>> exit()

   # Или используйте Flask-Migrate (рекомендуется)
   flask db init
   flask db migrate -m "Initial migration"
   flask db upgrade

   # Запустите сервер разработки Flask
   # Сервер будет доступен по адресу http://localhost:5000
   flask run
   ```

3. **Настройка фронтенда**
   ```bash
   # Откройте новый терминал в корне проекта
   cd frontend

   # Установите зависимости
   npm install

   # Запустите сервер разработки React
   # Обычно доступен по адресу http://localhost:3000
   npm run dev
   ```

4. **Запуск через Docker (альтернатива для продакшена)**
   ```bash
   # Из корня проекта
   docker-compose up -d
   ```

## Структура базы данных (MVP)

### Основные сущности (SQLAlchemy Models)

**Пользователь (User)**
- `id`: Integer (primary key)
- `email`: String(120), unique, nullable=False
- `password_hash`: String(200), nullable=False
- `created_at`: DateTime, default=datetime.utcnow

**Проект (Project)**
- `id`: Integer (primary key)
- `name`: String(100), nullable=False
- `description`: Text, nullable=True
- `owner_id`: Integer, ForeignKey('user.id'), nullable=False
- `created_at`: DateTime, default=datetime.utcnow

**Задача (Task)**
- `id`: Integer (primary key)
- `title`: String(200), nullable=False
- `description`: Text, nullable=True
- `deadline`: DateTime, nullable=True
- `status`: String(50), default='todo' (todo, in_progress, done, backlog)
- `priority`: String(20), default='medium' (low, medium, high, critical)
- `project_id`: Integer, ForeignKey('project.id'), nullable=False
- `assignee_id`: Integer, ForeignKey('user.id'), nullable=True
- `created_by_id`: Integer, ForeignKey('user.id'), nullable=False
- `created_at`: DateTime, default=datetime.utcnow
- `updated_at`: DateTime, default=datetime.utcnow, onupdate=datetime.utcnow

**Тег (Tag)**
- `id`: Integer (primary key)
- `name`: String(50), nullable=False
- `color`: String(7), default='#3498db' (HEX код)
- `project_id`: Integer, ForeignKey('project.id'), nullable=False

**Связь Задачи и Тега (task_tags)**
- `task_id`: Integer, ForeignKey('task.id'), primary_key=True
- `tag_id`: Integer, ForeignKey('tag.id'), primary_key=True

## API Эндпоинты (план)

Бэкенд будет построен как REST API. Примерные эндпоинты:

| Метод | Эндпоинт | Описание | Доступ |
|-------|----------|----------|--------|
| POST | `/api/auth/register` | Регистрация | Public |
| POST | `/api/auth/login` | Вход, получение JWT | Public |
| GET | `/api/projects` | Список проектов пользователя | Private |
| POST | `/api/projects` | Создать проект | Private |
| GET | `/api/projects/<id>` | Детали проекта | Private |
| PUT | `/api/projects/<id>` | Обновить проект | Private |
| DELETE | `/api/projects/<id>` | Удалить проект | Private |
| GET | `/api/projects/<id>/tasks` | Задачи проекта | Private |
| POST | `/api/tasks` | Создать задачу | Private |
| PUT | `/api/tasks/<id>` | Обновить задачу | Private |
| DELETE | `/api/tasks/<id>` | Удалить задачу | Private |
| GET | `/api/tags` | Список тегов | Private |
| POST | `/api/tags` | Создать тег | Private |
