# Спецификация типов данных MedFlow

## 1. Patient (Пациент)
| Поле | C# Type | SQL Type | Ограничения | Описание |
|---|---|---|---|---|
| Id | `int` | `INT` | PK, Identity | Первичный ключ |
| FirstName | `string` | `NVARCHAR(100)` | Required | Имя |
| LastName | `string` | `NVARCHAR(100)` | Required | Фамилия |
| MiddleName | `string?` | `NVARCHAR(100)` | Nullable | Отчество |
| BirthDate | `DateTime` | `DATETIME2` | Required | Дата рождения |
| Phone | `string` | `VARCHAR(20)` | Required, Unique | Телефон |
| Email | `string?` | `VARCHAR(255)` | Nullable, Unique | Email |
| PolicyNumber | `string?` | `VARCHAR(50)` | Nullable | Номер полиса ОМС/ДМС |
| Address | `string?` | `NVARCHAR(500)` | Nullable | Адрес регистрации |
| IsDeleted | `bool` | `BIT` | Default 0 | Флаг мягкого удаления |
| CreatedAt | `DateTime` | `DATETIME2` | Required | Дата создания записи |
| UpdatedAt | `DateTime?` | `DATETIME2` | Nullable | Дата последнего изменения |

## 2. Doctor (Врач)
| Поле | C# Type | SQL Type | Ограничения | Описание |
|---|---|---|---|---|
| Id | `int` | `INT` | PK, Identity | Первичный ключ |
| FirstName | `string` | `NVARCHAR(100)` | Required | Имя |
| LastName | `string` | `NVARCHAR(100)` | Required | Фамилия |
| MiddleName | `string?` | `NVARCHAR(100)` | Nullable | Отчество |
| Phone | `string` | `VARCHAR(20)` | Required | Рабочий телефон |
| Email | `string` | `VARCHAR(255)` | Required, Unique | Рабочий email |
| HireDate | `DateTime` | `DATETIME2` | Required | Дата трудоустройства |
| ExperienceYears | `int?` | `INT` | Nullable | Стаж в годах |
| IsDeleted | `bool` | `BIT` | Default 0 | Флаг мягкого удаления |
| CreatedAt | `DateTime` | `DATETIME2` | Required | Дата создания записи |

## 3. Service (Медицинская услуга)
| Поле | C# Type | SQL Type | Ограничения | Описание |
|---|---|---|---|---|
| Id | `int` | `INT` | PK, Identity | Первичный ключ |
| Name | `string` | `NVARCHAR(200)` | Required | Название услуги |
| Description | `string?` | `NVARCHAR(MAX)` | Nullable | Подробное описание |
| Price | `decimal` | `DECIMAL(18,2)` | Required, >= 0 | Стоимость услуги |
| DurationMinutes | `int` | `INT` | Required, > 0 | Длительность в минутах |
| IsActive | `bool` | `BIT` | Default 1 | Доступна ли для записи |
| CreatedAt | `DateTime` | `DATETIME2` | Required | Дата добавления в прайс |

## 4. Appointment (Запись на приём)
| Поле | C# Type | SQL Type | Ограничения | Описание |
|---|---|---|---|---|
| Id | `int` | `INT` | PK, Identity | Первичный ключ |
| PatientId | `int` | `INT` | FK -> Patient.Id | Ссылка на пациента |
| DoctorId | `int` | `INT` | FK -> Doctor.Id | Ссылка на врача |
| ServiceId | `int` | `INT` | FK -> Service.Id | Ссылка на услугу |
| AppointmentDate | `DateTime` | `DATETIME2` | Required | Дата и время начала приёма |
| Status | `int` | `INT` | Required | 0=Запланировано, 1=Завершено, 2=Отменено, 3=Не явился |
| Notes | `string?` | `NVARCHAR(1000)` | Nullable | Примечание регистратора или врача |
| CreatedAt | `DateTime` | `DATETIME2` | Required | Дата создания записи |