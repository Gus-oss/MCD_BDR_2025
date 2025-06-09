# Modelo entidad relación. 

_*Objetivos:*_
- Convertir la base de datos no estructurada en un modelo entidad-relación , representandolo con un diagrama entidad-relación.
- Mostrar el dominio de los atributos.

## Modelo entidad-relación de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
La base de datos de Covid-19 seleccionada es la base historica con fecha de publicación del 27 de Mayo del 2025. A continuación se mostrara su correspondiente diagrama entidad-relación

```mermaid
erDiagram
    PACIENTE ||--|| UBICACION : Radica
    PACIENTE ||-- || SERVICIOS_SALUD: Atendido
    PACIENTE ||--o{ COMORBILIDADES : Padece 
    PACIENTE ||-- || DIAGNOSTICO: Tiene
    PACIENTE {
        string ID_REGISTRO
        date FECHA_ACTUALIZACION
        date FECHA_INGRESO 
        date FECHA_SINTOMAS
        string FECHA_DEF
        int SEXO    
        int EDAD
        int EMBARAZO
        int NACIONALIDAD
        int HABLA_LENGUA_INDIG
        int INDIGENA
        int MIGRANTE    

    }

    UBICACION
    UBICACION {
        int ENTIDAD_NAC
        int ENTIDAD_RES
        int MUNICIPIO_RES
        int PAIS_NACIONALIDAD
        int PAIS_ORIGEN

    }

    SERVICIOS_SALUD
    SERVICIOS_SALUD {
        int ORIGEN
        int SECTOR
        int ENTIDAD_UM
        int TIPO_PACIENTE


    }

    COMORBILIDADES  
    COMORBILIDADES  {
        int Intubado
        int Neumonia
        int Diabetes
        int EPOC
        int ASMA
        int INMUSUPR
        int HIPERTENCION
        int CARDIOVASCULAR
        int OBESIDAD
        int RENAL_CRONICA
        int TABAQUISMO
    }

    DIAGNOSTICO
    DIAGNOSTICO {
        int TOMA_MUESTRA_LAB
        int  RESULTADO_PCR 
        int RESULTADO_PCR_COINFECCION
        int TOMA_MUESTRA_ANTIGENO
        int RESULTADO_ANTIGENO
        int CLASIFICACION_FINAL_COVID
        int CLASIFICACION_FINAL_FLU
        int UCI
        int OTRO_CASO


    }
````

Cabe mencionar que la base de datos se encuentra codificada mediante un catalago, por este motivo la mayoria de las variables de la base de datos son de caracter entero.

## Dominio de los atributos.

En esta sección se mostrara un ejemplo de una muestra de la base de datos.

| **Atributo**     | **Dominio**                           |
|--------------|---------------------------------------|
|*FECHA_ACTUALIZACION*   | '27/05/2025'     |
|*ID_REGISTRO*     | "167f1a"         |
|*ORIGEN*    | "1"; Usmer                        |
|*SECTOR*        | "12" ;SSA        |
|*ENTIDAD_UM*         | "1"; Aguascalientes          |
|*SEXO*        | "2"; Hombre      |
|*ENTIDAD_NAC*      | "1"; Aguascalientes                  |
|*ENTIDAD_RES*      | "1"; Aguascalientes              |
|*MUNICIPIO_RES*      | "3";Calvillo                  |
|*TIPO_PACIENTE*      | "1";Ambulatorio                   |
|*FECHA_INGRESO*      | "21/04/2025"                |
|*FECHA_SINTOMAS*      | "20/04/2025"               |
|*FECHA_DEF*      | "9999-99-99";No especificado                  |
|*INTUBADO*      | "97" ; No aplica             |
|*NEUMONIA*      | "2"; No                   |
|*EDAD*      | "8"                   |
|*NACIONALIDAD*      | "1"; Mexicana                |
|*EMBARAZO*      | "97"; No aplica                |
|*HABLA_LENGUA_INDIG* | "2"; No |
|*INDIGENA* | "2"; No | 
|*DIABETES* | "2"; No |
|*EPOC* | "2"; No | 
|*ASMA* | "2"; No | 
|*INMUSUPR* | "2"; No | 
|*HIPERTENSION* | "2"; No | 
|*OTRA_COM* | "2"; No |
|*CARDIOVASCULAR* | "2"; No | 
|*OBESIDAD* | "2"; No | 
|*RENAL_CRONICA* | "2"; No | 
|*TABAQUISMO* | "2"; No | 
|*OTRO_CASO* | "2"; No |
|*TOMA_MUESTRA_LAB* | "2"; No |
|*RESULTADO_PCR* | "997" ; No aplica (caso sin muestra) |
|*RESULTADO_PCR_COINFECCION* | "997"; No aplica (caso sin muestra) |
|*TOMA_MUESTRA_ANTIGENO* | "2"; No aplica |
|*RESULTADO_ANTIGENO* | "97" | 
|*CLASIFICACION_FINAL_COVID* | "6" | 
|*CLASIFICACION_FINAL_FLU* | "6" |
|*MIGRANTE* | "99" | 
|*PAIS_NACIONALIDAD* | "Méxicana" | 
|*PAIS_ORIGEN* | "97" | 
|*UCI* | "97" | 