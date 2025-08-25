# 📌 Tablas y Relaciones (PK y FK)



### Tabla `company_data`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| company_name    | VARCHAR(255)    | NOT NULL, UNIQUE                                |
| company_logo    | VARCHAR(255)    | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |

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

### Tabla `roles`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                     |
| name            | VARCHAR(255)    | NOT NULL                                        |
| guard_name      | VARCHAR(255)    | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |

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


