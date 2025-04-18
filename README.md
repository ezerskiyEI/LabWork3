# Лабораторная работа № 3

**Курс:** ПнаЯВУ  
**Группа:** 334702  
**Вариант:** № 2  
**ФИО:** Езерский Е.И.

![папич-артас](https://github.com/ezerskiyEI/LabWork2/raw/main/%D0%BF%D0%B0%D0%BF%D0%B8%D1%87-%D0%B0%D1%80%D1%82%D0%B0%D1%81.gif)

## Описание

В данной лабораторной работе реализован сервис для управления информацией об автомобилях и их владельцах. Сервис предоставляет RESTful API для выполнения CRUD-операций, таких как добавление, получение, обновление и удаление информации об автомобилях и владельцах. Приложение разработано с использованием Spring Boot и использует PostgreSQL для хранения данных.

## Изменеия

Реализована связь @ManyToMany между сущностями CarInfo и Owner, позволяющая каждому владельцу быть привязанным к нескольким автомобилям и наоборот.
Добавлены кастомные SQL-запросы с параметрами с использованием аннотации @Query. Например, реализован запрос для получения списка автомобилей по имени владельца.
Добавлен простой in-memory кэш, реализованный в компоненте EntityCache. Он использует Map<String, Object> для хранения недавно полученных сущностей (например, CarInfo, Owner) и ускорения доступа к данным без повторных запросов в базу данных.
Добавлены дополнительные endpoint'ы:
Поиск автомобиля по имени владельца.
Обновление данных по VIN или ID.
Удаление сущностей с очисткой соответствующего кэша.

### Сервис для управления автомобилями:

- Реализован класс-контроллер `CarInfoController`, который обрабатывает запросы по управлению информацией об автомобилях.
- Добавлен класс `CarInfo`, представляющий модель информации об автомобиле с полями VIN, марка, модель и год выпуска.
- Реализован класс `CarInfoService`, который содержит бизнес-логику для работы с данными об автомобилях.

### Сервис для управления владельцами:

OwnerController — контроллер для обработки HTTP-запросов по управлению владельцами автомобилей.

Owner — модель данных для представления информации о владельце, включая:

уникальный идентификатор (ID),

имя (name),

список автомобилей, которыми владеет данный человек.

OwnerService — сервисный слой, содержащий бизнес-логику для работы с владельцами автомобилей.

## CRUD-операции  и поддерживаемые эндпоинты

Работа с автомобилями:

Получение всех автомобилей:
GET /cars
Возвращает список всех автомобилей.

Получение информации об автомобиле по VIN:
GET /cars/{vin}
Возвращает информацию об автомобиле с указанным VIN (если автомобиль существует).

Добавление нового автомобиля:
POST /cars

Обновление информации об автомобиле по VIN:
PUT /cars/{vin}
Позволяет обновить информацию об автомобиле с указанным VIN. Требуется передать обновленные данные.

Удаление автомобиля по VIN:
DELETE /cars/{vin}
Удаляет автомобиль с указанным VIN.

Работа с владельцами:
Получение всех владельцев:
GET /owners
Возвращает список всех владельцев.

Получение информации о владельце по ID:
GET /owners/{id}
Возвращает информацию о владельце с указанным ID.

Добавление нового владельца:
POST /owners
Позволяет добавить нового владельца. Требуется передать данные в формате JSON:

Обновление информации о владельце:
PUT /owners/{id}
Позволяет обновить информацию о владельце с указанным ID.

Удаление владельца по ID:
DELETE /owners/{id}
Удаляет владельца с указанным ID.

Добавление автомобиля владельцу:
POST /owners/{ownerId}/cars/{vin}
Позволяет связать автомобиль с владельцем. Требуется указать ID владельца и VIN автомобиля.

## Использование

Для работы с сервисом можно использовать Postman или любой другой HTTP-клиент. Приложение поддерживает следующие операции:

- Получение информации обо всех автомобилях.
- Получение информации об автомобиле по VIN.
- Добавление нового автомобиля.
- Удаление автомобиля по VIN.
- Получение информации обо всех владельцах.
- Добавление нового владельца.

## Задание

В рамках лабораторной работы были выполнены следующие задачи:
Настроена база данных PostgreSQL
Реализованы сущности CarInfo и Owner с Many-to-Many связью
Добавлены REST-контроллеры и сервисы
Реализованы CRUD-операции для всех сущностей
Добавлен кэш (Map)
Добавлен кастомный @Query с параметром
