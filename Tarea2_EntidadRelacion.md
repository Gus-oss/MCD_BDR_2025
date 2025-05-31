# Modelo entidad relación. 

_*Objetivos:*_
- Convertir la base de datos no estructurada en un modelo entidad-relación , representandolo con un diagrama entidad-relación.
- Mostrar el dominio de los atributos.

## Modelo entidad-relación de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
La base de datos de Covid-19 seleccionada es la base historica con fecha de publicación del 27 de Mayo del 2025. 

```mermaid
erDiagram
    PACIENTE ||--o{ COMORBILIDADES : places
    PACIENTE ||--o{ UBICACION : is
    PACIENTE ||--o{ SERVICIOS_SALUD: is
    PACIENTE ||--o{ DIAGNOSTICO: is
    PACIENTE {
        string ID_REGISTRO       
        string ORIGEN
        string sector
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
````

