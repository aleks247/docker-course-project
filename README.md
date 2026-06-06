# Е-commerce Платформа за Дрехи (Clothing Brand Project)

Този проект представлява пълнофункционално уеб приложение (E-commerce магазин за дрехи), изградено с модерен технологичен стек и изцяло контейнеризирано с помощта на Docker и Docker Compose.

---

## 1. Архитектура и Структура на Проекта

Проектът е разделен на два основни независими модула (Бекенд и Фронтенд) и контейнеризирана база данни:

```text
CLOTHING BRAND/
│
├── clothing-brand-backend/        # Бекенд модул (Spring Boot)
│   ├── src/main/java/e_commerce/clothing_brand/
│   │   ├── config/                # Сигурност (JWT) и CORS конфигурации
│   │   ├── controller/            # REST Контролери (API endpoints)
│   │   ├── dto/                   # Data Transfer Objects
│   │   ├── entity/                # JPA Ентитита (User, Order, Product)
│   │   ├── enums/                 # Енумерации за роли и статуси
│   │   ├── mapper/                # Компоненти за мапване на обекти
│   │   ├── repository/            # Слой за комуникация с базата данни
│   │   ├── security/              # Логика за JWT валидация и филтри
│   │   └── service/               # Бизнес логика на приложението
│   ├── src/main/resources/        # Конфигурационни файлове (application.properties)
│   ├── Dockerfile                 # Инструкции за контейнеризация на Бекенда
│   └── pom.xml                    # Maven зависимостти
│
├── clothing-brand-frontend/       # Фронтенд модул (React + Vite)
│   ├── src/
│   │   ├── auth/                  # Компоненти и логика за автентикация
│   │   ├── components/            # Общи UI компоненти (Navbar, Footer, ProductCard, Table)
│   │   ├── contexts/              # Споделено състояние (AuthContext, CartContext)
│   │   ├── routes/                # Страници и маршрути (Home, Catalog, Profile, Admin, Orders)
│   │   ├── styles/                # CSS/Стилизиране на приложението
│   │   ├── utils/                 # Помощни функции и скриптове
│   │   ├── App.jsx                # Главен React компонент
│   │   └── main.jsx               # Входна точка за Vite
│   ├── Dockerfile                 # Инструкции за контейнеризация на Фронтенда
│   └── package.json               # Зависимости и скриптове на Node.js
│
└── compose.yml                    # Главен Docker Compose конфигурационен файл
```
---
## 2. Технологичен Стек
Фронтенд: React 19, Vite (Сървър за разработка), React Router v7, Context API за състоянието (Количка и Потребител).

Бекенд: Java 21, Spring Boot 3.x, Spring Security (JWT автентикация), Spring Data JPA / Hibernate.

База Данни: MySQL 8.0.

Оркестрация: Docker & Docker Compose.

## 3. Комуникация и Сигурност в Системата
1.Мрежа на Docker: Всички услуги са свързани в изолирана виртуална мрежа (app-network). Бекендът комуникира с базата данни директно в контейнерната мрежа чрез адрес: jdbc:mysql://db:3306/ecommerce.

2.CORS и Портове:

  * Фронтендът работи на порт 3000 и е достъпен на http://localhost:3000.

  * Бекендът работи на порт 8081 и е достъпен на http://localhost:8081.

  * В SecurityConfig на Spring Boot изрично е разрешен CORS достъп за http://localhost:3000, включително експортиране на Authorization хедъра за JWT токените.

3.Автоматично Стартиране: Използван е механизъм за healthcheck при MySQL контейнера, който гарантира, че Spring Boot стартира автоматично едва след като базата данни е напълно готова да приема връзки.


## 4. Как се изгражда и стартира проектът
### Предварителни изисквания:
  * Инсталиран и работещ Docker Desktop.

### Стъпки:
#### 1. Клонирайте хранилището и отворете терминал в неговата главна папка (където е файлът compose.yml).

#### 2. Стартирайте изграждането на образите и контейнерите със следната команда:

```

docker compose up --build

```
#### 3. Docker Compose автоматично ще извърши следните действия:

   * Ще свали и подготви MySQL 8.0 на порт 3306.

   * Ще изчака базата данни да стане healthy.

   * Ще компилира Java кода на бекенда и ще го пусне на порт 8081.

   * Ще инсталира node_modules и ще пусне Vite фронтенда на порт 3000.

### Адреси за достъп:
##### Магазин (React UI): http://localhost:3000

##### Бекенд API: http://localhost:8081

### За спиране на контейнерите използвайте: 
```

docker compose down

```
## 5. Линк към Публикуваните Образи в Docker Hub
### Всички готови за deployment контейнерни образи са качени публично в Docker Hub:
👉 Линк към Docker Hub Профилът ми: https://hub.docker.com/u/aleks247

Бекенд образ: aleks247/spring-backend:latest

Фронтенд образ: aleks247/react-frontend:latest

---

### Роли и задачи:
  * 22202 - Lead Engieer (DevOps, docker compose engineer)- Написва compose.yml, дефинира услугите clothing-brand-frontend, clothing-brand-backend и mysql
  * 22222 - Developer - Уверява се, че проекта работи локало, написа Dockerfile за Frontend и Backend components
  * 22211 - QA & Release Engineer - Локален тестинг на приложението за изправност на чужда машина, разписва документацията на проекта и се занимава с git
