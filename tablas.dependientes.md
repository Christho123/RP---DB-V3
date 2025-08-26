# 🔗 Tablas Dependientes

Estas tablas dependen de otras entidades mediante **llaves foráneas**.  
Definen relaciones y estructuras clave del sistema.

---

### Tabla `users`

|   Atributos        |   Tipo de Dato  |              Restricciones                   |
|--------------------|-----------------|----------------------------------------------|
| id                 | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| document_number    | VARCHAR(255)    | NOT NULL, UNIQUE                             |
| photo_url          | VARCHAR(255)    | NULL                                         |
| name               | VARCHAR(255)    | NOT NULL                                     |
| paternal_lastname  | VARCHAR(255)    | NOT NULL                                     |
| maternal_lastname  | VARCHAR(255)    | NOT NULL                                     |
| email              | VARCHAR(255)    | NOT NULL, UNIQUEL                            |
| sex                | char(1)         | NOT NULL, CHECK (sex IN ('M','F'))           |
| phone              | VARCHAR(100)    | NULL                                         |
| user_name          | VARCHAR(150)    | NOT NULL, UNIQUE                             |
| password           | VARCHAR(150)    | NOT NULL                          |
| password_change    | TINYINT(1)      | NOT NULL                                         |
| last_session       | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
| account_statement  | TINYINT(1)      | NOT NULL, DEFAULT 'A', CHECK (account_statement IN ('A','I')) |
| email_verified_at  | TIMESTAMP       | NULL                                         |
| document_type_id   | BIGINT(20)      | NOT NULL, FOREIGN KEY → document_types(id)   |
| country_id         | INT(20)         | NULL                                         |
| remenber_token     | VARCHAR(100)    | DEFAULT CURRENT_TIMESTAMP                    |
| created_at         | TIMESTAMP       | NULL                                         |
| updated_at         | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |
| deleted_at         | TIMESTAMP       | NULL                                         |

---
- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `document_type_id` → `document_types(id)`
  - `country_id` → `countries(id)`
- 📌 Restricciones:
  - `document_number`, `email`, `user_name` son **únicos**.
  - `sex` → CHECK(`M`, `F`)
  - `account_statement` → CHECK(`A`, `I`)
---

### Tabla `users_verification_codes`

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

---

- 🔑 **PK:** `id`
- 🔗 **FK:** `user_id` → `users(id)` (**1:1** relación).
- 📌 Maneja códigos de verificación, expiración y bloqueos.

---

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

- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `document_type_id` → `document_types(id)`
  - `region_id` → `regions(id)`
  - `province_id` → `provinces(id)`
  - `district_id` → `districts(id)`

---

### Tabla `patients`

|       Atributos        |   Tipo de Dato  |              Restricciones                   |
|------------------------|-----------------|----------------------------------------------|
| id                     | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| document_number        | VARCHAR(20)     | NOT NULL                                     |
| document_type_id       | INT             | NOT NULL, FK → document_types(id)            |
| paternal_lastname      | VARCHAR(150)    | NOT NULL                                     |
| maternal_lastname      | VARCHAR(150)    | NOT NULL                                     |
| first_name             | VARCHAR(150)    | NOT NULL                                     |
| personal_reference     | VARCHAR(255)    | NULL                                         |
| birth_date             | DATE            | NULL                                         |
| sex                    | VARCHAR(50)     | NULL                                         |
| primary_phone          | VARCHAR(80)     | NOT NULL                                     |
| secondary_phone        | VARCHAR(80)     | NULL                                         |
| email                  | VARCHAR(255)    | NOT NULL                                     |
| ocupation              | VARCHAR(100)    | NULL                                         |
| health_condition       | VARCHAR(255)    | NULL                                         |
| address                | VARCHAR(255)    | NULL                                         |
| country_id             | INT             | NOT NULL                                     |
| region_id              | INT             | NOT NULL, FK → regions(id)                   |
| province_id            | INT             | NOT NULL, FK → provinces(id)                 |
| district_id            | INT             | NOT NULL, FK → districts(id)                 |
| address                | TEXT            | NULL                                         |
| created_at             | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at             | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at             | TIMESTAMP       | NULL                                         |

---

- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `document_type_id` → `document_types(id)`
  - `country_id` → `countries(id)`
  - `region_id` → `regions(id)`
  - `province_id` → `provinces(id)`
  - `district_id` → `districts(id)`

---

### Tabla `medical_records`
|   Atributos     |   Tipo de Dato  |              Restricciones                   |
|-----------------|-----------------|----------------------------------------------|
| id              | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| patient_id      | INT             | NOT NULL, FK → patient(id)                   |
| diagnoses_id    | INT             | NOT NULL, FK → diagnoses(id)                 |
| diagnoses_date  | DATE            |                                              |
| symptoms        | TEXT            | NULL                                         |
| treatment       | TEXT            | NULL                                         |
| notes           | TEXT            | NOT NULL, FK → diagnoses(id)                 |
| status          | VARCHAR(20)     | DEFAULT → active                             |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at      | TIMESTAMP       | NULL                                         |

---

- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `patient_id` → `patients(id)`
  - `diagnoses_id` → `diagnoses(id)`
- 📌 Relación **1:N** (un paciente puede tener varios registros médicos).

---

### Tabla `appointments`

|       Atributos         |   Tipo de Dato  |              Restricciones                   |
|-------------------------|-----------------|----------------------------------------------|
| id                      | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| patients_id             | INT             | NOT NULL, FK → patients(id)                  |
| therapists_id           | INT             | NULL, FK → patients(id)                      |
| appointment_date        | DATE            | NULL                                         |
| appointment_hour        | TIME            | NULL                                         |
| ailments                | TEXT            | NULL                                         |
| diagnosis               | TEXT            | NULL                                         |
| surgeries               | TEXT            | NULL                                         |
| reflexology_diagnostics | TEXT            | NULL                                         |
| medications             | TEXT            | NULL                                         |
| observation             | TEXT            | NULL                                         |
| initial_date            | DATE            | NULL                                         |
| final_date              | DATE            | NULL                                         |
| appointment_type        | VARCHAR(100)    | NULL                                         |
| room                    | VARCHAR(50)     | NULL                                         |
| social_benefit          | VARCHAR(100)    | NULL                                         |
| payment_detail          | TEXT            | NULL                                         |
| payment                 | DECIMAL         | NULL                                         |
| ticket_number           | VARCHAR(50)     | NULL                                         |
| appointment_status_id   | INT             | NOT NULL, FK → appointment_status(id)        |
| payment_types_id        | INT             | NOT NULL, FK → payment_types(id)             |
| created_at              | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at              | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| delete_at               | TIMESTAMP       | NULL                                         |
| is_active               | TINYINT(1)      | NOT NULL, DEFAULT 1                          |

---

- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `patients_id` → `patients(id)`
  - `therapists_id` → `therapists(id)`
  - `appointment_status_id` → `appointment_statuses(id)`
  - `payment_types_id` → `payment_types(id)`
- 📌 Relación central entre pacientes, terapeutas y pagos.

---

### Tabla `provinces`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| region_id     | INT             | NOT NULL, FK → regions(id) ON DELETE CASCADE ON UPDATE CASCADE |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

- 🔑 **PK:** `id`
- 🔗 **FK:** `region_id` → `regions(id)`  
  *(con ON DELETE/UPDATE CASCADE)*

---

### Tabla `districts`
`

|   Atributos   |   Tipo de Dato  |              Restricciones                   |
|---------------|-----------------|----------------------------------------------|
| id            | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| name          | VARCHAR(255)    | NOT NULL                                     |
| province_id   | INT             | NOT NULL, FK → provinces(id) ON DELETE CASCADE ON UPDATE CASCADE |
| created_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at    | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at    | TIMESTAMP       | NULL                                         |

---

- 🔑 **PK:** `id`
- 🔗 **FK:** `province_id` → `provinces(id)`  
  *(con ON DELETE/UPDATE CASCADE)*

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

---

- 🔑 **PK:** `id`
- 🔗 **FK:** `country_id` → `countries(id)`  
  *(con ON DELETE/UPDATE CASCADE)*

---

### Tabla `tickets`

|   Atributos       |   Tipo de Dato  |              Restricciones                   |
|-------------------|-----------------|----------------------------------------------|
| id                | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| appointment_id    | INT             | NOT NULL, FK → appointment(id)               |
| ticket_number     | VARCHAR(50)     | NULL, UNIQUE                                 |
| payment_date      | DATETIME        | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP|
| amount            | DECIMAL         | (10,2)                                       |
| payment_types_id  | INT             | NULL, FOREIGN KEY → payment_types(id)        |
| description       | TEXT            | NULL                                         |
| status            | VARCHAR(20)     | NULL, FOREIGN KEY → payment_types(id)        |
| created_at        | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at        | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| is_active         | TINYINT(1)      | NOT NULL, DEFAULT 1                          |

---

- 🔑 **PK:** `id`
- 🔗 **FKs:**
  - `appointment_id` → `appointments(id)`
  - `payment_types_id` → `payment_types(id)`
- 🔐 Campo único: `ticket_number`

---

### Tabla `histories`

|   Atributos          |   Tipo de Dato  |              Restricciones                   |
|----------------------|-----------------|----------------------------------------------|
| id                   | INT             | PRIMARY KEY, AUTO_INCREMENT                  |
| document_types_id    | INT             | NOT NULL, FK → document_types(id)            |
| document_number      | VARCHAR(50)     | NOT NULL                                     |
| testimony            | TEXT            | NULL                                         |
| private_observation  | TEXT            | NULL                                         |
| observation          | TEXT            | NULL                                         |
| height               | DECIMAL         | (5,2), NULL                                  |
| weight               | DECIMAL         | (5,2), NULL                                  |
| last_weight          | DECIMAL         | (5,2), NULL                                  |
| created_at           | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                    |
| updated_at           | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| deleted_at           | TIMESTAMP       | NULL                                         |

---

- 🔑 **PK:** `id`
- 🔗 **FK:** `document_types_id` → `document_types(id)`
- 📌 Guarda historial clínico general de pacientes.

---

### Tabla `role_has_permissions`
|   Atributos     |   Tipo de Dato  |              Restricciones                      |
|-----------------|-----------------|-------------------------------------------------|
| permissions_id  | INT             | NOT NULL                                        |
| roles_id        | INT             | NOT NULL                                        |
| detail          | TEXT            | NULL                                            |
| created_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP                       |
| updated_at      | TIMESTAMP       | DEFAULT CURRENT_TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP |
| updated_at      | TIMESTAMP       | NULL                                            |

---

- 🔑 **PK Compuesta:** (`permissions_id`, `roles_id`)
- 🔗 **FKs:**
  - `permissions_id` → `permissions(id)`
  - `roles_id` → `roles(id)`
- 📌 Define relación **N:M** entre `roles` y `permissions`.

---

### Tabla `user_profiles`

PENDIENTE--

