#  Consultas

## Objetivos
1- Usar funciones de agregación para calcular en la base de datos: 
- Conteo de frecuencias 
- mínimo o máximos 
- cuantil cuyo resultado sea distinto a la mediana
- moda
- reportar hallazgos, dificultades, implementación de soluciones encontradas en linea, etc.


2- Hacer por lo menos un ejemplo de cada una de estas consultas

## Consultas de la base de datos Covid-19.

### Consultas basicas
Proyeccion de  todos los registros de la tabla
 ```sql 
 SELECT * FROM covid19mexico2025;
  ```
Proyección de los primeros 10 registros de la tabla
 ```sql 
 SELECT * FROM covid19mexico2025
 limit 10;
  ```
Proyeccion de los atributos de las columnas seleccionadas
 ```sql 
 SELECT ID_REGISTRO,SEXO, ENTIDAD_NAC
 FROM covid19mexico2025
 limit 10;
  ```
Proyeccion de la columna ID_REGISTRO renombrada temporalmente como Registro
 ```sql 
 SELECT ID_REGISTRO AS Registro
 FROM covid19mexico2025
 limit 10;
  ```
Proyeccion de 10 filas a partir de la fila 5  de la columna ID_REGISTRO
 ```sql 
 SELECT ID_REGISTRO
 FROM covid19mexico2025
 limit 4, 10; #limit n-1 , 10 donde n= 5
  ```
### Consultas con where
Proyección de los ID_REGISTRO cuando la columna SEXO e INTUBADO son iguales a 1
 ```sql 
 SELECT ID_REGISTRO, SEXO, INTUBADO
 FROM covid19mexico2025
 where (SEXO = 1
 AND INTUBADO = 2    
 );
  ```
### Consultas por agrupación
Conteo de filas de la columna ID_REGISTRO
 ```sql 
 SELECT ID_REGISTRO, COUNT(*) FROM covid19mexico2025
 group by ID_REGISTRO;
  ```
Contamos las entidades con mayor casos de covid-19 y las ordenamos en orden asendente
 ```sql 
 SELECT ENTIDAD_UM, COUNT(*) FROM covid19mexico2025
 group by ENTIDAD_UM
 order by ENTIDAD_UM ASC;
  ```
## Dificultades
La mayoria de las columnas de la base de datos del Covid-19 son de caracteristicas categoricas, por lo cual se es dificil encontrar algunas funciones estadisticas.