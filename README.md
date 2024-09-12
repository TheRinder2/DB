# Платформа онлайн курсов
# Чопчиц Дмитрий Андреевич
# 253501
# Online Learning Platform Database Schema

This database schema is designed for an online learning platform, supporting various features such as course management, user accounts, content delivery, and social interactions.

## Table Structure

### 1. Course (Курс)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the course |
| Title        | VARCHAR(255)  | Course title |
| Description  | TEXT          | Course description |
| Price        | DECIMAL(10, 2)| Course price |
| Duration     | INT           | Course duration in hours |

### 2. User (Пользователь)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the user |
| Username     | VARCHAR(50)   | User name |
| Email        | VARCHAR(100)  | Email address |
| PasswordHash | VARCHAR(255)  | Hashed password |
| Role         | ENUM('student', 'teacher', 'admin') | User role |

### 3. Instructor (Преподаватель)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the instructor |
| Name         | VARCHAR(100)  | Instructor name |
| Bio          | TEXT          | Instructor biography |
| Experience   | INT           | Years of experience as an instructor |

### 4. Category (Категория)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the category |
| Name         | VARCHAR(50)    | Category name |
| Description  | TEXT          | Category description |

### 5. Topic (Тема)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the topic |
| Name         | VARCHAR(50)    | Topic name |
| Description  | TEXT          | Topic description |

### 6. Chapter (Глава)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the chapter |
| Title        | VARCHAR(100)  | Chapter title |
| Content      | TEXT          | Chapter content |
| Order        | INT           | Chapter order in the course |

### 7. Lesson (Урок)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the lesson |
| Title        | VARCHAR(100)  | Lesson title |
| Content      | TEXT          | Lesson content |
| Type         | ENUM('video', 'text', 'interactive') | Lesson type |
| Order        | INT           | Lesson order in the chapter |

### 8. Assignment (Задание)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the assignment |
| Title        | VARCHAR(100)  | Assignment title |
| Description  | TEXT          | Assignment description |
| Type         | ENUM('test', 'project', 'review') | Assignment type |
| Deadline     | DATE          | Assignment deadline |

### 9. Review (Отзыв)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for the review |
| Rating       | TINYINT        | Course rating (1-5) |
| Comment      | TEXT          | Review comment |
| CourseID    | INT           | Identifier of the related course (FOREIGN KEY) |
| UserID       | INT           | Identifier of the user who left the review (FOREIGN KEY) |

### 10. Enrollment (Регистрация на курс)

| Field        | Data Type     | Description |
|--------------|---------------|-------------|
| ID           | INT PRIMARY KEY | Unique identifier for enrollment |
| CourseID     | INT           | Identifier of the enrolled course (FOREIGN KEY) |
| UserID       | INT           | Identifier of the user (FOREIGN KEY) |
| EnrollmentDate | DATE         | Date of enrollment |
| Status      | ENUM('active', 'completed', 'cancelled') | Enrollment status |