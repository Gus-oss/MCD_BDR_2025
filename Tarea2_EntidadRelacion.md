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

_*Notas:*_
- Falta añadir la parte del dominio, preguntar si se la tengo que agregar al diagrama o al documento. 