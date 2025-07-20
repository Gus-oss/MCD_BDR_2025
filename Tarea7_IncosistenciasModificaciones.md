# Inconsistencias de errores y subconsultas

## Objetivos.
- Revisas inconsistencias en la base de datos
- Hacer modificaciones o ajustes que faciliten la manipulacion de la base de datos usando lenguaje SQL
- Utilizar subconsultas para responder preguntas relevantes de los datos

## Revision de invonsistencias en la base de datos.

Revisamos si hay alguna inconsistencia entre la fecha de inicio de sintoams y la defunción de los pacientes 
 ```sql 
 SELECT ID_REGISTRO, FECHA_SINTOMAS, FECHA_DEF
 FROM covid19mexico2025 c
 WHERE FECHA_SINTOMAS > FECHA_DEF;
  ```
El resultado fueron las columnas ID_REGISTRO, FECHA_SINTOMAS, FECHA_DEF completamente vacias, lo que indica que no hay inconsistencias en estas fechas. 

Posteriormente se consultaron si hay valores nulos el sus resultados 
 ```sql 
 SELECT ID_REGISTRO
 FROM covid19mexico2025 c
 WHERE RESULTADO_PCR IS NULL AND RESULTADO_ANTIGENO IS NULL;
  ```
El resultado de esta consulta es vacio, lo que indica que no hay valores nulos en estas columnas.

Verificamos que no existan registros negativos en la variable edad
 ```sql 
 SELECT ID_REGISTRO, SEXO
 FROM covid19mexico2025 c
 WHERE EDAD < 0 ;
  ```
El resultado obtenido fue que en el conjunto de datos no se cuenta con valores negativos respecto a la edad de las personas. 

## Subconsultas para el análisis de datos

Consultamos los pacientes fallecidos con mayor edad por entidad
 ```sql 
 WITH max_por_estado AS (
  SELECT 
    ID_REGISTRO,
    EDAD,
    ENTIDAD_RES,
    ROW_NUMBER() OVER (PARTITION BY ENTIDAD_RES ORDER BY EDAD DESC, ID_REGISTRO) AS fila
  FROM covid19mexico2025
  WHERE FECHA_DEF IS NOT NULL
)
SELECT ID_REGISTRO, EDAD, ENTIDAD_RES
FROM max_por_estado
WHERE fila = 1
ORDER BY ENTIDAD_RES;
  ```
El resultado fueron el ID_REGISTRO de los pacientes de la base de datos, su edad y la entidad en la que reciden. Se muestran los resultados de manera creciente de acuerdo a la ENTIDAD_RES. La persona con mayor edad fue en el estado de Aguascalientes.

