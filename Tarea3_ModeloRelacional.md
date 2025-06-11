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

## Operaciones del algebra relacional. 

Algunas operaciónes del algebra relacional que se utilizaran para la base de datos de Covid-19 son: selección, proyección, unión y join.

### Selección.
*Consulta:* Obtener los pacientes del sexo femenino que tienen obesidad.

*Expresión:* $\sigma_{\text{SEXO} = 1 \land \text{OBESIDAD} = 1} \left( \text{PACIENTE} \bowtie \text{PACIENTE\_COMORBILIDAD} \bowtie \text{COMORBILIDADES} \right)$

*Explicación:*

### Proyección.
*Consulta:* Obtener únicamente los identificadores de los registros y las edades de los pacientes registrados.

*Expresión:* 
$$
\displaystyle
 \left (\pi_{\text{ID\_REGISTRO},\text{EDAD}}(\text{PACIENTE}) \right)
$$


*Explicación:

### Unión
*Consulta:* Obtener todos los pacientes que tienen diabetes o hipertensión

*Expresión:* $ \pi_{\text{ID\_REGISTRO}}(\sigma_{\text{DIABETES}=1}(\text{COMORBILIDADES})) \cup  \pi_{\text{ID\_REGISTRO}}(\sigma_{\text{HIPERTENCION}=1}(\text{COMORBILIDADES})) $

*Explicación:

### Join
*Consulta:* Obtener información combinada de los pacientes y el sector de salud donde fueron atendidos. 

*Expresión:* $ \text{PACIENTE} \bowtie \text{SERVICIOS\_SALUD} $

*Explicación:


Math block:

$$
\pi_{\text{ID\_REGISTRO}, \text{EDAD}} 
\leq 
\left( \sum_{k=1}^n a_k^2 \right) 
\left( \sum_{k=1}^n b_k^2 \right)
$$

