# 🗄️ Tablas Independientes

Estas son tablas maestras o catálogos que sirven de base para otras entidades.  
No dependen de otras tablas mediante llaves foráneas.

### Tabla `table_company_data`

|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| company_name    | VARCHAR(255)    | NOT NULL, UNIQUE                                |
| company_logo    | VARCHAR(255)    | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
---
- 🔑 **PK:** `id`
- 📌 Información general de la empresa.
- ⚡ Sin llaves foráneas.
---

### Tabla `appointment_statuses`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| name            | VARCHAR(255)    | NOT NULL                                        |
| description     | TEXT            | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| is_active       | TINYINT(1)      | NULL                                             |

---
- 🔑 **PK:** `id`
- 📌 Define los diferentes **estados de las citas**.
- ⚡ Sin llaves foráneas.
- ✔️ Campo importante: `is_active`.
---
### Tabla `roles`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| name            | VARCHAR(255)    | NOT NULL                                        |
| guard_name      | VARCHAR(255)    | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |

---
- 🔑 **PK:** `id`
- 📌 Contiene los roles del sistema (admin, user, etc.).
- ⚡ Sin llaves foráneas.
---

### Tabla `payment_types`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(50)     | NOT NULL, UNIQUE                             |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---
- 🔑 **PK:** `id`
- 📌 Lista de **tipos de pago** (efectivo, tarjeta, transferencia).
- ⚡ Sin llaves foráneas.
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

---
- 🔑 **PK:** `id`
- 📌 Lista de **países**.
- 📌 Campos relevantes: `ISO2`, `phone_code`.
- ⚡ Sin llaves foráneas.
---

### Tabla `document_types`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| description   | VARCHAR(255)    | NULL |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---
- 🔑 **PK:** `id`
- 📌 Catálogo de **tipos de documentos** (DNI, pasaporte, etc.).
- ⚡ Sin llaves foráneas.
---

### Tabla `diagnoses`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| code          | VARCHAR(10)     | NOT NULL, UNIQUE                             |
| name          | VARCHAR(255)    | NOT NULL                                     |
| description   | TEXT            | NULL                                         |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---
- 🔑 **PK:** `id`
- 📌 Catálogo de **diagnósticos médicos**.
- 🔐 Campo único: `code`.
- ⚡ Sin llaves foráneas.
---

### Tabla `predetermined_prices`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| price         | VARCHAR(255)    | NULL                                         |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---
- 🔑 **PK:** `id`
- 📌 Define precios predeterminados para servicios.
- ⚡ Sin llaves foráneas.
---
