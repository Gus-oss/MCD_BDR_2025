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
  