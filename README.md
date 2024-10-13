# Платформа онлайн курсов
## Чопчиц Дмитрий Андреевич
### 253501

## Функциональные требования

### 1. Управление курсами

- Создание новых курсов с возможностью выбора категории и темы
- Изменение информации о курсе (описание, цена, длительность)
- Удаление курсов
- Организация курсов в категории и темы

### 2. Управление пользователями

- Регистрация новых пользователей
- Аутентификация пользователей
- Обновление профилей пользователей
- Удаление аккаунтов пользователей

### 3. Управление преподавателями

- Добавление новых преподавателей
- Изменение информации о преподавателях
- Удаление преподавателей
- Назначение преподавателей к курсам

### 4. Управление учебным материалом

- Добавление уроков к курсам
- Изменение содержимого уроков
- Удаление уроков
- Организация учебного материала в иерархической структуре

### 5. Управление заданиями и тестами

- Создание заданий и тестов для курсов
- Выпуск заданий и тестов для студентов
- Оценка ответов студентов
- Подсчет итоговых баллов

### 6. Управление отзывами

- Оставление отзывов о курсах
- Публикация отзывов
- Удаление отзывов (при необходимости)
- Оценка качества курсов на основе отзывов

### 7. Управление регистрацией на курсы

- Просмотр доступных курсов
- Регистрация на курсы
- Отмена регистрации на курсы
- Отслеживание статуса регистрации пользователей

### 8. Управление административными функциями

- Просмотр общего состояния системы
- Управление правами доступа пользователей
- Обнаружение и обработка ошибок

### 9. Журналирование  действий пользователя
- Запись всех действий пользователя
- А так же запись даты и краткое описание действия


## Table Structure

### 1. Course (Курс)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the course |
| Title        | VARCHAR(255)  | Course title |
| Description  | TEXT          | Course description |
| Price        | DECIMAL(10, 2)| Course price |
| StartDate    | Date           | Course start time |
| EndDate      | Date           | Course end time |

### 2. User (Пользователь)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the user |
| Username     | VARCHAR(30)   | User name |
| Email        | VARCHAR(100)  | Email address |
| PasswordHash | VARCHAR(255)  | Hashed password |
| Role         | ENUM('student', 'teacher', 'admin') | User role |

### 3. UserProfile (Профиль)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| UserID       | INT FOREIGN KEY| Unique identifier for the user |
| FirstName    | VARCHAR(50)   | First name |
| LastNam      | VARCHAR(50)   | Last Name |
| BirthDate    | DateTime      | Date of birth |

### 4. Instructor (Преподаватель)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the instructor |
| Name         | VARCHAR(50)  | Instructor name |
| Bio          | TEXT          | Instructor biography |
| Experience   | TEXT          | Years of experience as an instructor |

### 5. Category (Категория)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the category |
| Title        | VARCHAR(50)    | Category name |
| Description  | TEXT          | Category description |

### 6. Lesson (Урок)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY| Unique identifier for the lesson |
| Title        | VARCHAR(100)  | Lesson title |
| ContentUR    | TEXT          | Lesson content |
| TypeId       | INT FOREIGN KEY| Lesson type |
| OrderPos     | INT           | Lesson order in the chapter |

### 7. LessonType (Тип урока)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the lesson |
| Name         | VARCHAR(50)   | Lesson title |
| Duration     | INT           | Lesson duration in hours|

### 8. Assignment (Задание)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY| Unique identifier for the assignment |
| Title        | VARCHAR(50)   | Assignment title |
| Description  | TEXT          | Assignment description |
| TypeID       | INT FOREIGN KEY| Assignment type |
| Deadline     | DATE          | Assignment deadline |

### 9. Review (Отзыв)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the review |
| Rating       | TINYINT        | Course rating (1-5) |
| Comment      | TEXT          | Review comment |
| CourseID     | INT FOREIGN KEY| Identifier of the related course |
| UserID       | INT FOREIGN KEY| Identifier of the user who left the review |

### 10. Enrollment (Регистрация на курс)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| CourseID     | INT FOREIGN KEY| Identifier of the enrolled course |
| UserID       | INT FOREIGN KEY| Identifier of the user |
| Date         | DATE           | Date of enrollment |
| StatusTypeID | INT FOREIGN KEY| Enrollment statustype |

### 10. Statustype (Статус регистрации на курс)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for Statustype |
| title        | VARCHAR(50)   | Status of course |

### 11. Action (Действия пользователя)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for action |
| UserID       | INT FOREIGN KEY| Identifier of the user |
| TimeStamp    | TimeStamp     | Date of action |
| ActionType   | Enum          | type of action |
| Description  | TEXT          | Аction description |

## Взаимосвязи

Следующие взаимосвязи существуют между таблицами:

### 1. Одно ко одному: User и Instructor

- Инструктор является также пользователем, но не все пользователи являются инструкторами.
- Эта связь позволяет легко идентифицировать преподавательский персонал в системе.

### 2. Одно ко многим: Course и Lessons

- Каждый курс может иметь несколько глав и уроков.
- Главы содержат уроки, создавая иерархическую структуру для контента курса.

### 3. Многие ко многим: User и Course

- Пользователи могут зарегистрироваться на нескольких курсах.
- Курсы могут иметь множество зарегистрированных пользователей.
- Эта связь поддерживает основную функциональность платформы обучения.

### 4. Одно ко многим: User и Action

- Пользователи могут множество действий.
- Каждое действие соверешено конкретным пользователем.
- Эта связь поддерживает журнал событий платформы обучения.

### 5. Многие ко многим: Instructor и Course

- Инструкторы могут преподавать несколько курсов.
- Курсы могут иметь множество инструкторов.
- Эта связь позволяет организовывать совместное обучение.

### 6. Одно ко многим: Course и Reviews

- Каждый курс может получить множество отзывов от пользователей.
- Отзывы ассоциируются со конкретными курсами.

### 7. Одно ко многим: User и Enrollments

- Каждый пользователь может иметь множество записей о регистрации в разных курсах.
- Записи о регистрации отслеживают участие пользователей в курсах во времени.

### 8. Одно ко многим: Course и Assignments

- Каждый курс может иметь множество заданий.
- Задания используются для оценки прогресса и понимания студентов.