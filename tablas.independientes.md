# 📌 Tablas y Relaciones (PK y FK)

### Tabla `permission`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| name            | VARCHAR(255)    | NOT NULL                                        |
| code_name       | VARCHAR(255)    | NOT NULL, UNIQUE                                |
| content_type_id | INT             | NOT NULL, FOREIGN KEY → django_content_type(id) |
| detail          | TEXT            | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| is_active       | TINYINT(1)      | NULL                                         |

### Tabla `role`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| name            | VARCHAR(255)    | NOT NULL                                        |
| description     | TEXT            | NULL                                            |
| content_type_id | INT             | NOT NULL, FOREIGN KEY → django_content_type(id) |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| is_active       | TINYINT(1)      | NULL                                             |


### Tabla `payments_types`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(50)     | NOT NULL, UNIQUE                             |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del tipo de pago.
- **FK**
  - Ninguna.

---

### Tabla `document_types`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(50)     | NOT NULL, UNIQUE                             |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del tipo de documento.
- **FK**
  - Ninguna.

---

### Tabla `countries`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| phone_code    | VARCHAR(10)     | NULL                                         |
| ISO2          | CHAR(2)         | NULL, UNIQUE                                 |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único del país.
- **FK**
  - Ninguna.

---

### Tabla `regions`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| country_id    | INT             | NOT NULL, FK → countries(id) ON DELETE CASCADE ON UPDATE CASCADE |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

###### 🔑 `Claves`
- **PK**
  - `id` → Identificador único de la región.
- **FK**
  - `country_id` → Referencia a **`countries(id)`**  
    - `ON DELETE CASCADE` → Si se elimina un país, se eliminan sus regiones.  
    - `ON UPDATE CASCADE` → Si cambia el ID del país, se actualiza en regiones.  



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

