# Modelo entidad relación. 

_*Objetivos:*_
- Convertir la base de datos no estructurada en un modelo entidad-relación , representandolo con un diagrama entidad-relación.
- Mostrar el dominio de los atributos.

## Modelo entidad-relación de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
La base de datos de Covid-19 seleccionada es la base historica con fecha de publicación del 27 de Mayo del 2025. 

```mermaid
erDiagram
    PACIENTE ||-- || UBICACION : tiene
    PACIENTE ||-- || SERVICIOS_SALUD: is
    PACIENTE ||--o{ COMORBILIDADES : padece  
    PACIENTE ||-- || DIAGNOSTICO: tiene
    PACIENTE {
        string ID_REGISTRO
        string FECHA_ACTUALIZACION
        string FECHA_INGRESO 
        string FECHA_SINTOMAS
        string FECHA_DEF
        string SEXO    
        string EDAD
        string EMBARAZO
        string NACIONALIDAD
        string HABLA_LENGUA_INDIG
        string INDIGENA
        string MIGRANTE    

    }

    UBICACION
    UBICACION {
        string ENTIDAD_NAC
        string ENTIDAD_RES
        string MUNICIPIO_RES
        string PAIS_NACIONALIDAD
        string PAIS_ORIGEN

    }

    SERVICIOS_SALUD
    SERVICIOS_SALUD {
        string ORIGEN
        string SECTOR
        string ENTIDAD_UM
        string TIPO_PACIENTE


    }

    COMORBILIDADES  
    COMORBILIDADES  {
        int Intubado
        string Neumonia
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
        string TOMA_MUESTRA_LAB
        string  RESULTADO_PCR 
        string RESULTADO_PCR_COINFECCION
        string TOMA_MUESTRA_ANTIGENO
        string RESULTADO_ANTIGENO
        string CLASIFICACION_FINAL_COVID
        string CLASIFICACION_FINAL_FLU
        string UCI
        string OTRO_CASO


    }
````

