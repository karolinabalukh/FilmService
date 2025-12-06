# 🎬 Film Service REST API

## Інструкція із запуску

### Передумови
- Встановлений **PostgreSQL**
- Створена порожня база даних з наступними параметрами:
    - **Database Name:** `film_db`
    - **Username:** `postgres` (можна змінити в `application.properties`)
    - **Password:** `root` (можна змінити в `application.properties`)

### Процес запуску
1. Запустіть додаток
2. Liquibase автоматично виконає:
    - Створення таблиць `directors` та `films`
    - Наповнення таблиці `directors` початковими даними

---

##  Тестування API (Postman)

## 1.  Отримання списку режисерів
Перевірка коректного створення початкових даних Liquibase.

**URL:** `http://localhost:8080/api/directors`  
**Method:** `GET`

**Очікуваний результат (200 OK):**
```json
[
  { "id": 1, "name": "Christopher Nolan", "..." },
  { "id": 2, "name": "Steven Spielberg", "..." },
  { "id": 3, "name": "Quentin Tarantino", "..." }
]
```

![](images\tests.png)



## 2.  Створення фільму
**URL:** `http://localhost:8080/api/films`  
**Method:** `POST`  
**Headers:** `Content-Type: application/json`

**Body:**
```json
{
  "title": "Inception",
  "year": 2010,
  "duration": 148,
  "genre": "Sci-Fi",
  "rating": 8.8,
  "description": "A thief who steals corporate secrets through the use of dream-sharing technology.",
  "directorId": 1
}
```
![](images\add_film.png)



## 3. Upload JSON
Завантаження списку фільмів з JSON-файлу.

**URL:** `http://localhost:8080/api/films/upload`  
**Method:** `POST`  
**Body Type:** `form-data`  
**Key:** `file` (Тип: File) → Виберіть файл `import_films.json`

**Приклад файлу `import_films.json`:**
```json
[
  {
    "title": "Wicked",
    "year": 2024,
    "duration": 160,
    "genre": "fairy tale",
    "rating": 7.4,
    "directorId": 1
  },
  {
    "title": "The Godfather",
    "year": 1972,
    "duration": 177,
    "genre": "crime",
    "rating": 9.2,
    "directorId": 2
  }
]
```
![](images\upload.png)

## 4.Отримання списку з пагінацією (_list)
Отримання відфільтрованих даних з пагінацією.

**URL:** `http://localhost:8080/api/films/_list`  
**Method:** `POST`

**Body:**
```json
{
  "page": 0,
  "size": 10,
  "directorId": 1
}
```
![](images\list.png)



## 5. Генерація звіту (_report)
Завантаження CSV-файлу з фільмами за вказаним фільтром.

**URL:** `http://localhost:8080/api/films/_report`  
**Method:** `POST`

**Body:**
```json
{
  "directorId": 1
}
```
![](images\report.png)
А також можливість завантажити файл через "Save response", як [films_report.csv](src%2Fmain%2Fresources%2Ffilms_report.csv)
![](images\excel_report.png)