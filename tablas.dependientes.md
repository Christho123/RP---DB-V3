### Tabla `users`

|   Atributos        |   Tipo de Dato  |              Restricciones                   |
|--------------------|-----------------|----------------------------------------------|
| id                 | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| document_number    | VARCHAR(255)    | NOT NULL, UNIQUE                             |
| photo_url          | VARCHAR(255)    | NULL                                         |
| name               | TIMESTAMP       | NOT NULL                                     |
| paternal_lastname  | TIMESTAMP       | NOT NULL                                     |
| maternal_lastname  | TIMESTAMP       | NULL                                         |
| email              | VARCHAR(255)    | NOT NULL, UNIQUEL                            |
| sex                | char(1)         | NOT NULL, CHECK (sex IN ('M','F'))           |
| phone              | VARCHAR(100)    | NULL                                         |
| user_name          | VARCHAR(150)    | NOT NULL, UNIQUE                             |
| password           | VARCHAR(150)    | NOT NULL                          |
| password_change    | TINYINT(1)      | NULL                                         |
| last_session       | DATEMTIME       | NULL |
| account_statement  | TINYINT(1)      | NOT NULL, DEFAULT 'A', CHECK (account_statement IN ('A','I')) |
| email_verified_at  | TIMESTAMP       | NULL                                         |
| document_type_id   | BIGINT(20)      | NOT NULL, FOREIGN KEY → document_types(id)   |
| country_id         | INT(20)         | NULL                                         |
| remenber_token     | VARCHAR(100)    | DEFAULT CURRENT_TIMESTAMP                    |
| created_at         | TIMESTAMP       | NULL                                         |
| updated_at         | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
| deleted_at         | TIMESTAMP       | NULL                                         |

### Tabla `users_verification_code`

|   Atributos        |   Tipo de Dato  |              Restricciones                   |
|--------------------|-----------------|----------------------------------------------|
| id                 | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| user_id            | BIGINT          | NOT NULL, UNIQUE, FOREIGN KEY → users(id)    |
| code               | VARCHAR(255)    | NULL                                         |
| expires_at         | TIMESTAMP       | NOT NULL                                     |
| failed_attempts    | INT(11)         | NOT NULL, DEFAULT 0                          |
| locked_until       | TIMESTAMP       | NULL                                         |
| created_at         | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at         | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP  |





### Tabla documen_types

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| description   | VARCHAR(255)    | NULL |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del tipo_documento.



### Tabla `therapists`

|       Atributos       |   Tipo de Dato  |              Restricciones                   |
|------------------------|-----------------|----------------------------------------------|
| id                     | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| document_type_id       | INT             | NOT NULL, FK → document_types(id)            |
| document_number        | VARCHAR(20)     | NOT NULL                                     |
| last_name_paternal     | VARCHAR(150)    | NOT NULL                                     |
| last_name_maternal     | VARCHAR(150)    | NOT NULL                                     |
| first_name             | VARCHAR(150)    | NOT NULL                                     |
| birth_date             | DATETIME        | NULL                                         |
| gender                 | VARCHAR(50)     | NULL                                         |
| personal_reference     | VARCHAR(255)    | NULL                                         |
| is_active              | TINYINT(1)      | NOT NULL, DEFAULT 1                          |
| phone                  | VARCHAR(20)     | NULL                                         |
| email                  | VARCHAR(254)    | NOT NULL                                     |
| region_id              | INT             | NOT NULL, FK → regions(id)                   |
| province_id            | INT             | NOT NULL, FK → provinces(id)                 |
| district_id            | INT             | NOT NULL, FK → districts(id)                 |
| address                | TEXT            | NULL                                         |
| profile_picture        | VARCHAR(255)    | NULL                                         |
| created_at             | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at             | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at             | TIMESTAMP       | NULL                                         |

---

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del terapeuta.
- **FK**
  - `document_type_id` → Referencia a **`document_types(id)`**  
  - `region_id` → Referencia a **`regions(id)`**  
  - `province_id` → Referencia a **`provinces(id)`**  
  - `district_id` → Referencia a **`districts(id)`**  

> ℹ️ En este caso, no se definió `ON DELETE CASCADE` para evitar borrar terapeutas si se elimina un ubigeo o un tipo de documento. Lo habitual es usar:
> - `ON UPDATE CASCADE`
> - `ON DELETE RESTRICT` o `SET NULL`

---


### Tabla provinces

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| region_id     | INT             | NOT NULL, FK → regions(id) ON DELETE CASCADE ON UPDATE CASCADE |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único de la provincia.
- **FK**
  - `region_id` → Referencia a **`regions(id)`**  
    - `ON DELETE CASCADE` → Si se elimina una región, se eliminan sus provincias.  
    - `ON UPDATE CASCADE` → Si cambia el ID de la región, se actualiza en provincias.  

---

### Tabla districts

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| province_id   | INT             | NOT NULL, FK → provinces(id) ON DELETE CASCADE ON UPDATE CASCADE |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del distrito.
- **FK**
  - `province_id` → Referencia a **`provinces(id)`**  
    - `ON DELETE CASCADE` → Si se elimina una provincia, se eliminan sus distritos.  
    - `ON UPDATE CASCADE` → Si cambia el ID de la provincia, se actualiza en distritos.  

---

### Tabla documen_types

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| description   | VARCHAR(255)    | NULL |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del tipo_documento.


---