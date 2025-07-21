# Joins

## Objetivos 
- Crear vistas (view) sobre consultas significativas, recurrentes, etc. que 
     - incluyan un Join
     - incluyan un Left Join 
     - incluyan un Right Join
     - incluyan una subconsulta
- Investigar y crear al menos un disparador (TRIGGER) de inserción, actualización o eliminación
- Elegir tema para Proyecto Integrador de Aprendizaje

## Creación de tablas de catalogos.
Como la base de datos de los pacientes de covid 19 se encuentra en solo una tabla, se tomo la decision de añadir las tablas correspondientes a los años 2020, 2021, 2022 y 2023 para realizar las vistas. Ademas de esto, se creo una tabla llamada cat_entidades, en la cual se encuentran la clave y las entidades que contienen dicha clave. El codigo utilizado fue el siguiente : 

 ```sql 
 CREATE TABLE cat_entidades (
  CLAVE_ENTIDAD INT PRIMARY KEY,
  ENTIDAD_FEDERATIVA VARCHAR(100) NOT NULL
);

INSERT INTO cat_entidades (CLAVE_ENTIDAD, ENTIDAD_FEDERATIVA) VALUES
(1, 'AGUASCALIENTES'),
(2, 'BAJA CALIFORNIA'),
(3, 'BAJA CALIFORNIA SUR'),
(4, 'CAMPECHE'),
(5, 'COAHUILA DE ZARAGOZA'),
(6, 'COLIMA'),
(7, 'CHIAPAS'),
(8, 'CHIHUAHUA'),
(9, 'CIUDAD DE MÉXICO'),
(10, 'DURANGO'),
(11, 'GUANAJUATO'),
(12, 'GUERRERO'),
(13, 'HIDALGO'),
(14, 'JALISCO'),
(15, 'MÉXICO'),
(16, 'MICHOACÁN DE OCAMPO'),
(17, 'MORELOS'),
(18, 'NAYARIT'),
(19, 'NUEVO LEÓN'),
(20, 'OAXACA'),
(21, 'PUEBLA'),
(22, 'QUERÉTARO'),
(23, 'QUINTANA ROO'),
(24, 'SAN LUIS POTOSÍ'),
(25, 'SINALOA'),
(26, 'SONORA'),
(27, 'TABASCO'),
(28, 'TAMAULIPAS'),
(29, 'TLAXCALA'),
(30, 'VERACRUZ DE IGNACIO DE LA LLAVE'),
(31, 'YUCATÁN'),
(32, 'ZACATECAS'),
(36, 'ESTADOS UNIDOS MEXICANOS'),
(97, 'NO APLICA'),
(98, 'SE IGNORA'),
(99, 'NO ESPECIFICADO');

  ```
Se añadieron tambien las siguientes tablas  para poder hacer joins entre las tablas de los distintos años y sus catalogos 

 ```sql 
#creacion de la tabla cat_origen

CREATE TABLE cat_ORIGEN (
  CLAVE INT,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_ORIGEN  (CLAVE , DESCRIPCION) VALUES
(1, 'USMER'),
(2, 'FUERA DE USMER'),
(99 , 'NO ESPECIFICADO'); 

ALTER TABLE cat_ORIGEN
ADD PRIMARY KEY (CLAVE);

#Creacion de la tabla cat_SECTOR
CREATE TABLE cat_SECTOR (
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_SECTOR (CLAVE , DESCRIPCION) VALUES
(1, 'CRUZ ROJA'),
(2, 'DIF'),
(3, 'ESTATAL'),
(4, 'IMSS'),
(5, 'IMSS-BIENESTAR'),
(6, 'ISSSTE'),
(7, 'MUNICIPAL'),
(8, 'PEMEX'),
(9, 'PRIVADA'),
(10, 'SEDENA'),
(11, 'SEMAR'),
(12, 'SSA'),
(13, 'UNIVERSITARIO'),
(14, 'CIJ'),
(15, 'IMSS Bienestar OPD'),
(99, 'NO ESPECIFICADO');

#Creacion de la tabla cat_Sexo
CREATE TABLE cat_sexo (
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_sexo  (CLAVE , DESCRIPCION) VALUES
(1, 'MUJER'),
(2, 'HOMBRE'),
(99 , 'NO ESPECIFICADO'); 

#Creacion de la tabla cat_tipo_paciente
CREATE TABLE cat_tipo_paciente(
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_tipo_paciente (CLAVE , DESCRIPCION) VALUES
(1, 'AMBULATORIO'),
(2, 'HOSPITALIZADO'),
(99 , 'NO ESPECIFICADO'); 

#Creacion de catalogo cat_si_no

CREATE TABLE cat_si_no(
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_si_no (CLAVE , DESCRIPCION) VALUES
(1, 'SI'),
(2, 'NO'),
(97, 'NO APLICA'),
(98, 'SE IGNORA'),
(99 , 'NO ESPECIFICADO'); 

#Creacion de catalogo  cat_nacionalidad

CREATE TABLE  cat_nacionalidad(
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO  cat_nacionalidad (CLAVE , DESCRIPCION) VALUES
(1, 'MEXICANA'),
(2, 'EXTRANJERA'),
(99 , 'NO ESPECIFICADO'); 

#Creacion catalogo cat_resultado_pcr

CREATE TABLE  cat_resultado_pcr(
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO cat_resultado_pcr (CLAVE , DESCRIPCION) VALUES
(1, 'INFLUENZA AH1N1 PMD'),
(2, 'INFLUENZA A H1'),
(3, 'INFLUENZA A H3'),
(4, 'INFLUENZA B'),
(5, 'NEGATIVO'),
(6, 'MUESTRA NO ADECUADA'),
(7, 'ADENOVIRUS'),
(8, 'PARAINFLUENZA 1'),
(9, 'PARAINFLUENZA 2'),
(10, 'PARAINFLUENZA 3'),
(11, 'VIRUS SINCICIAL RESPIRATORIO'),
(13, 'INFLUENZA A NO SUBTIPIFICADA'),
(14, 'INFLUENZA A H5'),
(17, 'MUESTRA RECHAZADA'),
(20, 'VIRUS SINCICIAL RESPIRATORIO A'),
(21, 'VIRUS SINCICIAL RESPIRATORIO B'),
(22, 'CORONA 229E'),
(23, 'CORONA OC43'),
(24, 'CORONA SARS'),
(25, 'CORONA NL63'),
(26, 'CORONA HKU1'),
(27, 'MUESTRA QUE NO AMPLIFICO'),
(28, 'ENTEROV//RHINOVIRUS'),
(29, 'METAPNEUMOVIRUS'),
(30, 'MUESTRA SIN AISLAMIENTO'),
(32, 'PARAINFLUENZA 4'),
(33, 'MUESTRA SIN CELULAS'),
(34, 'SARS-CoV-2'),
(35, 'MERS-CoV'),
(36, 'SARS-CoV'),
(37, 'BOCAVIRUS'),
(41, 'MUESTRA NO RECIBIDA'),
(997, 'NO APLICA (CASO SIN MUESTRA)'),
(998, 'SIN COINFECCIÓN'),
(999, 'PENDIENTE');

#Creacion de catalogo cat_resultado_antigeno

CREATE TABLE  cat_resultado_antigeno(
  CLAVE INT primary KEY,
  DESCRIPCION VARCHAR(100) NOT NULL
);

INSERT INTO  cat_resultado_antigeno (CLAVE , DESCRIPCION) VALUES
(1, 'POSITIVO A SARS-COV-2'),
(2, 'NEGATIVO A SARS-COV-2'),
(97 , 'NO APLICA (CASO SIN MUESTRA)'); 


#Creacion de catalogo cat_clasificacion_final

CREATE TABLE cat_CLASIFICACION_FINAL (
  CLAVE INT PRIMARY KEY,
  CLASIFICACION VARCHAR(150) NOT NULL,
  DESCRIPCION TEXT NOT NULL
);

INSERT INTO cat_CLASIFICACION_FINAL (CLAVE, CLASIFICACION, DESCRIPCION) VALUES
(1, 'CASO DE COVID-19 CONFIRMADO POR ASOCIACIÓN CLÍNICA EPIDEMIOLÓGICA',
 'Confirmado por asociación aplica cuando el caso informó ser contacto de un positivo a COVID-19 (y este se encuentra registrado en el SISVER) y: Al caso no se le tomó muestra ni de PCR ni de antígeno o la muestra resultó no válida.'),
(2, 'CASO DE COVID-19 CONFIRMADO POR COMITÉ DE  DICTAMINACIÓN',
 'Confirmado por dictaminación solo aplica para defunciones bajo las siguientes condiciones: Al caso no se le tomó muestra ni de PCR ni de antígeno o sí se tomó muestra, pero la muestra resultó no válida.'),
(3, 'CASO DE SARS-COV-2  CONFIRMADO',
 'Confirmado aplica cuando: El caso tiene muestra de laboratorio PCR o prueba antigénica y resultó positiva  a SARS-CoV-2, sin importar si el caso tiene asociación clínica epidemiológica.'),
(4, 'INVÁLIDO POR LABORATORIO',
 'Inválido aplica cuando el caso no tiene asociación clínico epidemiológica, ni dictaminación a COVID-19. Se le tomó muestra de laboratorio PCR y esta resultó no válida.'),
(5, 'NO REALIZADO POR LABORATORIO',
 'No realizado aplica cuando el caso no tiene asociación clínico epidemiológica, ni dictaminación a COVID-19 y se le tomó muestra de laboratorio PCR y esta no se procesó.'),
(6, 'CASO SOSPECHOSO',
 'Sospechoso aplica cuando: El caso no tiene asociación clínico epidemiológica, ni dictaminación a COVID-19 y no se le tomó muestra, o se le tomó muestra de laboratorio y está pendiente de resultado, sin importar otra condición.'),
(7, 'NEGATIVO A SARS-COV-2',
 'Negativo aplica cuando el caso: 1. Se le tomó muestra de laboratorio PCR y ésta resultó: negativa a SARS-COV-2 o positiva a cualquier otro virus respiratorio (Influenza, VSR, Bocavirus, otros) sin importar que este caso tenga asociación clínico epidemiológica o dictaminación a COVID-19. 2. Se le tomó muestra antigénica que resultó negativa a SARS-COV-2 y al caso no se le tomó muestra de laboratorio PCR ni se le confirmó por asociación epidemiológica o por dictaminación clínica epidemiológica.');

#Creacion de catalogo cat_clasificacion_final_flu

CREATE TABLE cat_clasificacion_final_flu (
  CLAVE INT PRIMARY KEY,
  CLASIFICACION VARCHAR(150) NOT NULL,
  DESCRIPCION TEXT NOT NULL
);
INSERT INTO cat_clasificacion_final_flu (CLAVE, CLASIFICACION, DESCRIPCION) VALUES
(3, 'CASO DE INFLUENZA CONFIRMADO', 
 'Confirmado aplica cuando el caso tiene muestra de laboratorio PCR y resultó positiva a Influenza.'),
(4, 'INVÁLIDO POR LABORATORIO', 
 'Inválido aplica cuando al caso se le tomó muestra de laboratorio PCR y esta resultó no válida.'),
(5, 'NO REALIZADO POR LABORATORIO', 
 'No realizado aplica cuando al caso se le tomó muestra de laboratorio PCR y esta no se procesó.'),
(6, 'CASO SOSPECHOSO', 
 'Sospechoso aplica cuando el caso no se le tomó muestra PCR, o se le tomó muestra de laboratorio PCR y está pendiente de resultado.'),
(7, 'NEGATIVO A INFLUENZA', 
 'Negativo aplica cuando al caso se le tomó muestra de laboratorio PCR y ésta resultó negativa a influenza o positiva a cualquier otro virus respiratorio.');

#Crear el catalogo cat_municipios
CREATE TABLE cat_municipios (
  CLAVE_ENTIDAD INT ,
  CLAVE_MUNICIPIO INT,
  MUNICIPIO VARCHAR (100)
);
```

## Inner Join 
Se crea una vista llamada vista_prom_edad_2025, en la cual se relaciona la tabla de casos de Covid-19 del año 2025 con el catálogo de entidades usando la clave de entidad para obtener el nombre del estado. Filtra los registros con edades válidad, entre 0 y 120 años y agrupa los resultados por entidad para calcular el promedio de edad de los pacientes por estado redondeando a una decimal. 

 ```sql 
 CREATE OR REPLACE VIEW vista_prom_edad_2025 AS
SELECT 
  e.ENTIDAD_FEDERATIVA,
  c.ENTIDAD_RES,
  ROUND(AVG(c.EDAD), 1) AS PROMEDIO_EDAD
FROM covid19mexico2025 c
INNER JOIN cat_entidades e ON c.ENTIDAD_RES = e.CLAVE_ENTIDAD
WHERE c.EDAD BETWEEN 0 AND 120
GROUP BY c.ENTIDAD_RES, e.ENTIDAD_FEDERATIVA;
```

## Left Join
El siguiente codigo hace una consulta convinada entre la tabla covid19mexico2020 y la tabla creada cat_origen y muestra la informacion de los primeros 100 registros de ambas columnas. 
 ```sql 
SELECT 
  c.ID_REGISTRO,
  c.ORIGEN,
  o.DESCRIPCION AS DESCRIPCION_ORIGEN
FROM covid19mexico2025 c
LEFT JOIN cat_ORIGEN o ON c.ORIGEN = o.CLAVE
LIMIT 100;
```

## Right Join
En esta consulta pedimos los primeros 100 registros que coincidad entre la columna sector de la taba covid19mexico2021 y la columna clave del catálogo cat_sector. Si no hay coincidencia en la tabla, el catálogo sí se mostrará completo.
 ```sql 
SELECT 
  c.ID_REGISTRO,
  c.SECTOR,
  s.DESCRIPCION AS DESCRIPCION_SECTOR
FROM covid19mexico2021 c
RIGHT JOIN cat_SECTOR s ON c.SECTOR = s.CLAVE
LIMIT 100;

```