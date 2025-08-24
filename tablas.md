
## Módulo 1 - Architect
Este módulo contiene toda la funcionalidad de autenticación, usuarios, permisos y roles del sistema, reorganizada en una estructura modular y mantenible.

### Tabla Base
---

|     Atributos    |   Tipo de Datos   |         Restricciones        |
|------------------|-------------------|------------------------------|
|id		           |    INT(20)        |                              |
|name              |    VARCHAR(255)   |                        |
|description       |    VARCHAR(255)   |                        |
|created_at        |    TIMESTAMP      |                        |
|updated_at        |    TIMESTAMP      |                        |
|deleted_at        |    TIMESTAMP      |                        |

---

| Atributos   | Tipo de Datos   | Restricciones                                         |
|-------------|-----------------|-------------------------------------------------------|
| created_at  | DATETIME        | DEFAULT CURRENT_TIMESTAMP                             |
| updated_at  | DATETIME        | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
| is_active   | TINYINT(1)      | DEFAULT 1                                             |

---

## Módulo 2 - 

## User

| **Atributos**        | **Tipos de Datos** | **Descripción** |
|----------------------|--------------------|-----------------|
| id                   | INT(20)            | PRIMARY KEY, AUTO_INCREMENT, NOT NULL |
| password             | VARCHAR(128)       | NOT NULL |
| last_login           | DATETIME(6)        | NULL (puede ser NULL hasta el primer login) |
| is_superuser         | TINYINT(1)         | NOT NULL, por defecto 0 (FALSE) |
| username             | VARCHAR(150)       | UNIQUE, NOT NULL, validación alfanumérica (máx. 150 caracteres) |
| first_name           | VARCHAR(150)       | NOT NULL, valores permitidos: 'M', 'F', 'O', 'P' |
| last_name            | VARCHAR(150)       | CNOT NULL |
| email                | VARCHAR(254)       | UNIQUE, NOT NULL |
| is_staff             | TINYINT(1)         | NOT NULL, por defecto 0 (FALSE) |
| is_active            | TINYINT(1)          | NOT NULL, por defecto 1 (TRUE) |
| receive_notifications| BOOLEAN (tinyint(1)) | NOT NULL, DEFAULT 1 |
| date_joined          | DATETIME(6)       | NOT NULL, se asigna automáticamente al crear el usuario |



--- 

## User Profiles

| **Atributos**        | **Tipos de Datos** | **Descripción** |
|----------------------|--------------------|-----------------|
| id                   | INT(20)           | PRIMARY KEY, AUTO_INCREMENT, NOT NULL |
| user_id              | BIGINT            | UNIQUE, FOREIGN KEY → users(id), NOT NULL, ON DELETE CASCADE|
| first_name           | VARCHAR(50)       | NOT NULL |
| paternal_lastname    | VARCHAR(50)       | NOT NULL |
| maternal_lastname    | VARCHAR(50)       | NOT NULL |
| gender               | CHAR(1)           | NOT NULL, valores permitidos: 'M', 'F', 'O', 'P' |
| email                | VARCHAR(254)      | CNOT NULL |
| is_public            | BOOLEAN           | NOT NULL, DEFAULT 1 |
| show_email           | BOOLEAN           | NOT NULL, DEFAULT 0 |
| show_phone           | BOOLEAN           | NOT NULL, DEFAULT 0 |
| receive_notifications| BOOLEAN (tinyint(1)) | NOT NULL, DEFAULT 1 |
| created_at           | DATETIME(6)       | NOT NULL, AUTO SET al crear |
| updated_at           | DATETIME(6)       | NOT NULL, AUTO UPDATE al modificar |






## Módulo 4 - Therapists

|Atributos:            |	   Tipo de Datos   |       Restricciones      |
|----------------------|-----------------------|--------------------------|
|id                    |      INT(20)          |                          |
|document_number,      |	  VARCHAR(20)	   |			              |
|last_name_paternal,   |	  VARCHAR(100)     |			              |
|last_name_maternal,   |	  VARCHAR(100)	   |			              |
|first_name,           |      VARCHAR(100)     |			              |
|birth_date,           |	  DATETIME	       |			              |
|gender,               |      VARCHAR(20)	   |		        	      |
|personal_references,  |	  VARCHAR(255)	   |		        	      |
|is_active,            |	  TINYINT(1)	   |		        	      |
|phone,                |	  VARCHAR(15)	   |		        	      |
|email,                |	  VARCHAR(255)	   |		        	      |
|country,              |	  VARCHAR(100)	   |		        	      |
|department,           |	  VARCHAR(100)	   |		        	      |
|province,             |	  VARCHAR(100)	   |		        	      |
|district,             |	  VARCHAR(100)	   |		        	      |
|address,              |	  TEXT		       |		        	      |
|profile_picture       |	  VARCHAR(255)	   |		        	      |





## Módulo 7 - Therapists


# Tablas - Ubicaciones

## Distrito

| **Atributos** | **Tipos de Datos** | **Descripción** |
|---------------|--------------------|-----------------|
| Id            | AutoField (PK)     | PRIMARY KEY, AUTO_INCREMENT, NOT NULL |
| name          | VARCHAR(20)        | NOT NULL |
| province      | VARCHAR(20)        | FOREIGN KEY → province(id), NOT NULL, ON DELETE CASCADE |
| deleted_at    | Date               | NULL permitido (para soft delete) |
| ubigeo_code   | INTEGER            | UNIQUE, NOT NULL, longitud 6 dígitos |
| created_at    | VARCHAR            | NOT NULL, DEFAULT CURRENT_TIMESTAMP |
| updated_at    | VARCHAR(20)        | NOT NULL, ON UPDATE CURRENT_TIMESTAMP |

---

## Province

| **Atributos** | **Tipos de Datos** | **Descripción** |
|---------------|--------------------|-----------------|
| Id            | AutoField (PK)     | PRIMARY KEY, AUTO_INCREMENT, NOT NULL |
| name          | CharField          | NOT NULL |
| región        | VARCHAR(20)        | FOREIGN KEY → region(id), NOT NULL, ON DELETE CASCADE |
| deleted_at    | DateTimeField      | NULL permitido (para soft delete) |
| ubigeo_code   | INTEGER            | UNIQUE, NOT NULL, longitud 4 dígitos |
| created_at    | DateTimeField      | NOT NULL, DEFAULT CURRENT_TIMESTAMP |
| updated_at    | DateTimeField      | NOT NULL, ON UPDATE CURRENT_TIMESTAMP |

---

## Región

| **Atributos** | **Tipos de Datos** | **Descripción** |
|---------------|--------------------|-----------------|
| Id            | AutoField (PK)     | PRIMARY KEY, AUTO_INCREMENT, NOT NULL |
| name          | CharField          | NOT NULL |
| deleted_at    | DateTimeField      | NULL permitido (para soft delete) |
| ubigeo_code   | INTEGER            | UNIQUE, NOT NULL, longitud 2 dígitos |
| created_at    | DateTimeField      | NOT NULL, DEFAULT CURRENT_TIMESTAMP |
| updated_at    | DateTimeField      | NOT NULL, ON UPDATE CURRENT_TIMESTAMP |