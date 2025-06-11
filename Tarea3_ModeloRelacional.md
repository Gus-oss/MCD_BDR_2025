# Modelo relacional. 

_*Objetivos:*_
- Crear un esquema del modelo relacional de la base de datos a partir del modelo e-r de la tarea anterior.
- Representar con un diagrama relacional tu esquema del punto anterior.
- Encontrar cuatro operaciones que se vaya a usar en la base de datos y expresarlas mediante operadores del álgebra relacional. Explica con nuestras propias palabras cada una de estas operaciones.

## Esquema del modelo relacional de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
Se mostrara a continuación las tablas de relaciones de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025.

### Tabla: PACIENTE

| Campo                  | Tipo     | Clave         |
|------------------------|----------|---------------|
| ID_REGISTRO           | STRING   | PRIMARY KEY   |
| FECHA_ACTUALIZACION   | DATE     |               |
| FECHA_INGRESO         | DATE     |               |
| FECHA_SINTOMAS        | DATE     |               |
| FECHA_DEF             | DATE     |               |
| SEXO                  | INT      | (catálogo)     |
| EDAD                  | INT      |               |
| EMBARAZO              | INT      | (catálogo)     |
| NACIONALIDAD          | INT      | (catálogo)     |
| HABLA_LENGUA_INDIG    | INT      | (catálogo)     |
| INDIGENA              | INT      | (catálogo)     |
| MIGRANTE              | INT      | (catálogo)     |
| ID_UBICACION          | FK → UBICACION(ID) |
| ID_SERVICIO           | FK → SERVICIOS_SALUD(ID) |
| ID_DIAGNOSTICO        | FK → DIAGNOSTICO(ID)     |

---

### Tabla: UBICACION

| Campo             | Tipo   | Clave       |
|-------------------|--------|-------------|
| ID                | INT    | PRIMARY KEY |
| ENTIDAD_NAC       | INT    | (catálogo)   |
| ENTIDAD_RES       | INT    | (catálogo)   |
| MUNICIPIO_RES     | INT    | (catálogo)   |
| PAIS_NACIONALIDAD | INT    | (catálogo)   |
| PAIS_ORIGEN       | INT    | (catálogo)   |

---

### Tabla: SERVICIOS_SALUD

| Campo         | Tipo   | Clave       |
|---------------|--------|-------------|
| ID            | INT    | PRIMARY KEY |
| ORIGEN        | INT    | (catálogo)   |
| SECTOR        | INT    | (catálogo)   |
| ENTIDAD_UM    | INT    | (catálogo)   |
| TIPO_PACIENTE | INT    | (catálogo)   |

---

### Tabla: DIAGNOSTICO

| Campo                        | Tipo   | Clave       |
|------------------------------|--------|-------------|
| ID                           | INT    | PRIMARY KEY |
| TOMA_MUESTRA_LAB             | INT    | (catálogo)   |
| RESULTADO_PCR                | INT    | (catálogo)   |
| RESULTADO_PCR_COINFECCION    | INT    | (catálogo)   |
| TOMA_MUESTRA_ANTIGENO        | INT    | (catálogo)   |
| RESULTADO_ANTIGENO           | INT    | (catálogo)   |
| CLASIFICACION_FINAL_COVID    | INT    | (catálogo)   |
| CLASIFICACION_FINAL_FLU      | INT    | (catálogo)   |
| UCI                          | INT    | (catálogo)   |
| OTRO_CASO                    | INT    | (catálogo)   |

---

### Tabla: COMORBILIDADES

| Campo            | Tipo   | Clave       |
|------------------|--------|-------------|
| ID               | INT    | PRIMARY KEY |
| INTUBADO         | INT    | (catálogo)   |
| NEUMONIA         | INT    | (catálogo)   |
| DIABETES         | INT    | (catálogo)   |
| EPOC             | INT    | (catálogo)   |
| ASMA             | INT    | (catálogo)   |
| INMUSUPR         | INT    | (catálogo)   |
| HIPERTENCION     | INT    | (catálogo)   |
| CARDIOVASCULAR   | INT    | (catálogo)   |
| OBESIDAD         | INT    | (catálogo)   |
| RENAL_CRONICA    | INT    | (catálogo)   |
| TABAQUISMO       | INT    | (catálogo)   |

---

### Tabla Relacional: PACIENTE_COMORBILIDAD

(Relación muchos a muchos entre PACIENTE y COMORBILIDADES)

| Campo           | Tipo   | Clave              |
|-----------------|--------|--------------------|
| ID_REGISTRO     | STRING | FK → PACIENTE      |
| ID_COMORBILIDAD | INT    | FK → COMORBILIDADES |
| PRIMARY KEY     | (ID_REGISTRO, ID_COMORBILIDAD) |

---