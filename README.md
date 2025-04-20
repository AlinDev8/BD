 Работа с базами данных PostgreSQL
Цель проекта:
Закрепление и углубление знаний, полученных в рамках курса по базам данных, через практическую работу с PostgreSQL. Проект включает создание, наполнение и управление данными в четырёх различных базах данных.

Общая структура проекта
Для каждой из четырёх баз данных предусмотрены:

Создание таблиц с указанием связей и ограничений.

Заполнение тестовыми данными.

Выполнение SQL-запросов для решения практических задач.

Все базы данных сопровождаются скриптами, автоматизирующими развёртывание структуры и загрузку демонстрационных данных.

1. База данных «Транспортные средства» (TransportDB)
Назначение: Учёт автомобилей, мотоциклов и велосипедов с детализацией характеристик.

Таблицы:
Vehicle (общая классификация):

maker – производитель.

model (PK) – уникальная модель.

type – тип: Car, Motorcycle, Bicycle.

Car (автомобили):

vin (PK) – идентификационный номер.

model (FK → Vehicle) – модель.

engine_capacity – объём двигателя (л).

horsepower – мощность (л.с.).

price – стоимость ($).

transmission – тип КП: Automatic/Manual.

Motorcycle (мотоциклы):

vin (PK) – идентификационный номер.

model (FK → Vehicle) – модель.

engine_capacity, horsepower, price – аналогично автомобилям.

type – тип: Sport, Cruiser, Touring.

Bicycle (велосипеды):

serial_number (PK) – серийный номер.

model (FK → Vehicle) – модель.

gear_count – количество передач.

price – стоимость ($).

type – тип: Mountain, Road, Hybrid.

Связи:
Таблицы Car, Motorcycle, Bicycle связаны с Vehicle через model.

2. База данных «Автомобильные гонки» (CarRacingDB)
Назначение: Учёт классов автомобилей, гонок и их результатов.

Таблицы:
Classes (классы автомобилей):

class (PK) – название (например, Formula 1).

type – тип: Racing/Street.

country – страна происхождения.

numDoors – количество дверей.

engineSize – объём двигателя (л).

weight – вес (кг).

Cars (модели автомобилей):

name (PK) – название модели.

class (FK → Classes) – класс.

year – год выпуска.

Races (гонки):

name (PK) – название гонки.

date – дата проведения.

Results (результаты):

car (FK → Cars) – модель автомобиля.

race (FK → Races) – гонка.

position – занятое место.

Связи:
Cars → Classes (классификация авто).

Results связывает Cars и Races.

3. База данных «Бронирование отелей» (BookingDB)
Назначение: Управление бронированиями номеров в отелях.

Таблицы:
Hotel (отели):

ID_hotel (SERIAL, PK) – идентификатор.

name, location – название и местоположение.

Room (номера):

ID_room (SERIAL, PK) – идентификатор.

ID_hotel (FK → Hotel) – отель.

room_type – тип: Single, Double, Suite.

price – стоимость ($).

capacity – вместимость.

Customer (клиенты):

ID_customer (SERIAL, PK) – идентификатор.

name, email, phone – контактные данные.

Booking (бронирования):

ID_booking (SERIAL, PK) – идентификатор.

ID_room (FK → Room), ID_customer (FK → Customer) – номер и клиент.

check_in_date, check_out_date – даты заезда/выезда.

Связи:
Room → Hotel (принадлежность номера).

Booking связывает Room и Customer.

4. База данных «Структура организации» (CompanyOrganizationDB)
Назначение: Управление сотрудниками, отделами и проектами компании.

Таблицы:
Departments (департаменты):

DepartmentID (PK) – идентификатор.

DepartmentName – название.

Roles (должности):

RoleID (PK) – идентификатор.

RoleName – название.

Employees (сотрудники):

EmployeeID (PK) – идентификатор.

Name, Position – имя и должность.

ManagerID (FK → Employees) – руководитель (ON DELETE SET NULL).

DepartmentID (FK → Departments, ON DELETE CASCADE) – отдел.

RoleID (FK → Roles, ON DELETE SET NULL) – роль.

Projects (проекты):

ProjectID (PK) – идентификатор.

ProjectName, StartDate, EndDate – данные проекта.

DepartmentID (FK → Departments, ON DELETE CASCADE) – отдел.

Tasks (задачи):

TaskID (PK) – идентификатор.

TaskName – название.

AssignedTo (FK → Employees, ON DELETE SET NULL) – исполнитель.

ProjectID (FK → Projects, ON DELETE CASCADE) – проект.

Связи:
Иерархия сотрудников через ManagerID.

Привязка проектов и задач к отделам (DepartmentID).

Связь задач с сотрудниками и проектами.

Итог:
Проект охватывает ключевые аспекты работы с PostgreSQL: проектирование схемы, настройку связей, наполнение данными и выполнение запросов. Каждая база данных решает конкретную бизнес-задачу, демонстрируя разнообразие подходов к структурированию информации.
