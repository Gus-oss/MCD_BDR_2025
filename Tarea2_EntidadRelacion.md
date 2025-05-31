# Modelo entidad relación. 

_*Objetivos:*_
- Convertir la base de datos no estructurada en un modelo entidad-relación , representandolo con un diagrama entidad-relación.
- Mostrar el dominio de los atributos.

## Modelo entidad-relación de la base de datos Covid-19 correspondiente a la fecha del 27 de Mayo del 2025. 
La base de datos de Covid-19 seleccionada es la base historica con fecha de publicación del 27 de Mayo del 2025. 

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
<pre> ```mermaid 
erDiagram PACIENTE ||--|| UBICACION : resides_in PACIENTE ||--|| SERVICIOS_SALUD : receives PACIENTE ||--|| COMORBILIDADES : has PACIENTE ||--|| DIAGNOSTICO : gets PACIENTE { string ID_REGISTRO int SEXO int EDAD string NACIONALIDAD int EMBARAZO } UBICACION { int ENTIDAD_RES int MUNICIPIO_RES int ENTIDAD_NAC string PAIS_NACIONALIDAD string PAIS_ORIGEN } SERVICIOS_SALUD { int SECTOR int ENTIDAD_UM int TIPO_PACIENTE } COMORBILIDADES { int DIABETES int EPOC int ASMA int INMUSUPR int HIPERTENSION int OBESIDAD int RENAL_CRONICA int TABAQUISMO } DIAGNOSTICO { int RESULTADO_PCR int RESULTADO_ANTIGENO int CLASIFICACION_FINAL_COVID int CLASIFICACION_FINAL_FLU int UCI } 
``` </pre>
