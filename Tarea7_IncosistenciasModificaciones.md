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

Consultamos cuantas personas por país hay en la base de datos 
 ```sql 
 SELECT 
  CASE 
    WHEN PAIS_ORIGEN = '97' THEN 'México'
    ELSE PAIS_ORIGEN
  END AS PAIS_NORMALIZADO,
  COUNT(*) AS TOTAL
FROM covid19mexico2025
WHERE PAIS_ORIGEN IS NOT NULL AND TRIM(PAIS_ORIGEN) <> ''
GROUP BY PAIS_NORMALIZADO
ORDER BY TOTAL DESC;
  ```
El resultado fue que hay un total de 92 pacientes de Colombia, 76 de Venezuela y 56 pacientes de Estados Unidos de América. Aunque a pesar de estos numeros hay 399,480 pacientes que no cuentan con un registro de su nacionalidad en la base de datos. 

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

Ahora se consultaran el promedio de edad de pacientes por sector de salud 
 ```sql 
SELECT 
  SECTOR, 
  ROUND(AVG(CAST(EDAD AS DECIMAL(5,2))), 2) AS PROM_EDAD
FROM covid19mexico2025
WHERE EDAD BETWEEN 0 AND 120
GROUP BY SECTOR
ORDER BY SECTOR;
  ```
El resultado de esta consulta fue el sector junto con su promedio de edad de sus pacientes. La edad promedio mas alta fue para PEMEX con una edad promedio de alrededor de 50. 

Haciendo la consulta para pacientes que fueron intubados y estan en UCI
 ```sql 
SELECT *
FROM covid19mexico2025
WHERE INTUBADO = 1 AND UCI = 1
ORDER BY FECHA_INGRESO ASC;
  ```
Esta consulta devuelve todos los pacientes que fueron intubados y estan en UCI ordenando de manera ascendente por la fecha de ingreso. 
