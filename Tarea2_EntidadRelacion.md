# Modelo entidad relación. 

_*Objetivos:*_
- Convertir la base de datos no estructurada en un modelo entidad-relación , representandolo con un diagrama entidad-relación.
- Mostrar el dominio de los atributos.

## Modelo entidad-relación de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
La base de datos de Covid-19 seleccionada es la base historica con fecha de publicación del 27 de Mayo del 2025. 

```mermaid
graph TD;
    PACIENTE["Paciente"]
    UBICACION["Ubicación"]
    SERVICIO["Servicio de Salud"]
    DIAGNOSTICO["Diagnóstico"]
    COMORBILIDADES["Comorbilidades"]

    PACIENTE --> UBICACION
    PACIENTE --> SERVICIO
    PACIENTE --> DIAGNOSTICO
    PACIENTE --> COMORBILIDADES

    UBICACION --> ENTIDAD_RES["Entidad de Residencia"]
    UBICACION --> MUNICIPIO_RES["Municipio de Residencia"]

    SERVICIO --> SECTOR["Sector"]
    SERVICIO --> ENTIDAD_UM["Entidad UM"]

    DIAGNOSTICO --> RESULTADO_PCR["Resultado PCR"]
    DIAGNOSTICO --> RESULTADO_ANTIGENO["Resultado Antígeno"]
    DIAGNOSTICO --> CLASIFICACION_FINAL_COVID["Clasificación COVID"]

    COMORBILIDADES --> DIABETES["Diabetes"]
    COMORBILIDADES --> ASMA["Asma"]
    COMORBILIDADES --> HIPERTENSION["Hipertensión"]
    COMORBILIDADES --> OBESIDAD["Obesidad"]

````

