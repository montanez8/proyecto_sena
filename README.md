## Carlos Montañez Rodriguez

# proyecto_sena
proyecto de bases de datos  de campuslands 2023 

## Modelo Entidad Relacion.

![Alt text](/archivos/EntidadRelacion.png)

## Modelo Relacional.

![Alt text](/archivos/modeloRelacional.png)


### Creacion de la base de datos.
```sql
    CREATE DATABASE proyecto_sena;
```
### Seleccion de la base de datos Proyecto_sena;
```sql
    USE proyecto_sena;
```
### Creacion de las tablas.
```sql
create table carreras
(
    id_carrera int auto_increment
        primary key,
    nombre     varchar(100) not null
);

create table cursos
(
    id_curso int auto_increment
        primary key,
    nombre   varchar(100) not null
);

create table especialidades
(
    id_especialidad int auto_increment
        primary key,
    nombre          varchar(100) not null
);

create table instructores
(
    id_instructor   int auto_increment
        primary key,
    nombre          varchar(100) not null,
    id_especialidad int          null,
    constraint instructores_id_especialidad_foreign
        foreign key (id_especialidad) references especialidades (id_especialidad)
);

create table matriculas
(
    id_matricula int auto_increment
        primary key
);

create table aprendices
(
    numero_documento int          not null
        primary key,
    nombre           varchar(100) not null,
    apellido         varchar(100) not null,
    id_carrera       int          not null,
    id_matricula     int          not null,
    constraint aprendices_ibfk_1
        foreign key (id_matricula) references matriculas (id_matricula),
    constraint aprendices_ibfk_2
        foreign key (id_carrera) references carreras (id_carrera)
);

create index id_carrera
    on aprendices (id_carrera);

create index id_matricula
    on aprendices (id_matricula);

create table rutas
(
    id_ruta    int auto_increment
        primary key,
    nombre     varchar(100) not null,
    id_carrera int          not null,
    constraint rutas_ibfk_1
        foreign key (id_carrera) references carreras (id_carrera)
);

create table curso_ruta
(
    id_curso int auto_increment,
    id_ruta  int not null,
    primary key (id_curso, id_ruta),
    constraint curso_ruta_ibfk_1
        foreign key (id_curso) references cursos (id_curso),
    constraint curso_ruta_ibfk_2
        foreign key (id_ruta) references rutas (id_ruta)
);

create index id_ruta
    on curso_ruta (id_ruta);

create table instructores_curso_ruta
(
    id_ruta       int not null,
    id_instructor int not null,
    id_curso      int not null,
    primary key (id_ruta, id_instructor, id_curso),
    constraint instructores_curso_ruta_ibfk_1
        foreign key (id_ruta) references rutas (id_ruta),
    constraint instructores_curso_ruta_ibfk_2
        foreign key (id_instructor) references instructores (id_instructor),
    constraint instructores_curso_ruta_ibfk_3
        foreign key (id_curso) references cursos (id_curso)
);

create index id_curso
    on instructores_curso_ruta (id_curso);

create index id_instructor
    on instructores_curso_ruta (id_instructor);

create index id_carrera
    on rutas (id_carrera);



```
### Poblar la base de datos.

- Tabla Carreras
```sql
INSERT INTO proyecto_sena.carreras (id_carrera, nombre) VALUES (1, 'Desarrollo de Software');
INSERT INTO proyecto_sena.carreras (id_carrera, nombre) VALUES (2, 'Electrónica ');
INSERT INTO proyecto_sena.carreras (id_carrera, nombre) VALUES (3, 'Macánica Automotriz ');
INSERT INTO proyecto_sena.carreras (id_carrera, nombre) VALUES (4, 'Seguridad y Salud Ocupacional ');
INSERT INTO proyecto_sena.carreras (id_carrera, nombre) VALUES (5, 'Soldadura ');

```
- Tabla matriculas
```sql
insert into matriculas(id_matricula) values(1);
insert into matriculas(id_matricula) values(2);
insert into matriculas(id_matricula) values(3);
insert into matriculas(id_matricula) values(4);
insert into matriculas(id_matricula) values(5);
insert into matriculas(id_matricula) values(6);
insert into matriculas(id_matricula) values(7);
insert into matriculas(id_matricula) values(8);
insert into matriculas(id_matricula) values(9);
insert into matriculas(id_matricula) values(10);

```
- Tabla Aprendices

```sql
-- Tabla Aprendices
INSERT INTO proyecto_sena.aprendices (numero_documento, nombre, apellido, id_carrera, id_matricula) VALUES
(123456789, 'Carlos', 'Gomez', 1, 1),
(234567890, 'Andrea', 'Martinez', 2, 2),
(345678901, 'Juan', 'Rodriguez', 3, 3),
(456789012, 'Laura', 'Perez', 4, 4),
(567890123, 'Diego', 'Hernandez', 5, 5),
(678901234, 'Camila', 'Lopez', 1, 6),
(789012345, 'Santiago', 'Garcia', 2, 7),
(890123456, 'Valentina', 'Sanchez', 3, 8),
(901234567, 'Alejandro', 'Diaz', 4, 9),
(123123123, 'Isabella', 'Vargas', 5, 10);

```
- Tabla Rutas
```sql
INSERT INTO proyecto_sena.rutas (id_ruta, nombre, id_carrera) VALUES
(1, 'Sistemas de Información Empresariales', 1),
(2, 'Videojuegos', 1),
(3, 'Machine Learning', 1),
(4, 'Microcontroladores', 2),
(5, 'Robótica', 2),
(6, 'Dispositivos Bio-médicos', 2),
(7, 'Motores Híbridos', 3),
(8, 'Vehículos de Uso Agrícola', 3),
(9, 'Sistemas de Gestión en Seguridad Ocupacional', 4),
(10, 'Soldadura Autógena Industrial', 5),
(11, 'Soldadura Eléctrica Industrial', 5),
(12, 'Soldadura Submarina', 5);

```
- Tabla Especialidades
```sql
INSERT INTO proyecto_sena.especialidades (nombre) VALUES
('Sistemas'),
('Salud Ocupacional'),
('Soldadura'),
('Mecánica'),
('Inglés'),
('Electrónica'),
('Electrónica'),
('Sistemas'),
('Sistemas'),
('Salud Ocupacional');
```

- Tabla instructores
```sql
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1029384756, 'Marinela Narvaez', 2);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1123456789, 'Ricardo Vicente Jaimes', 1);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1209384756, 'Roy Hernando Llamas', 5);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1345678901, 'Maria Jimena Monsalve', 6);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1567384920, 'Nelson Raúl Buitrago', 4);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1654327890, 'Andrea González', 9);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1765432980, 'Marisela Sevilla', 10);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1890347562, 'Juan Carlos Cobos', 7);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1948273645, 'Agustín Parra Granados', 3);
INSERT INTO proyecto_sena.instructores (numero_documento, nombre, id_especialidad) VALUES (1987654321, 'Pedro Nell Santoamaría', 8);

```
- Tabla Cursos
```sql
insert into cursos(id_curso,nombre) values(1,'Matemáticas Básicas');
insert into cursos(id_curso,nombre) values(2,'Álgebra Computacional');
insert into cursos(id_curso,nombre) values(3,'Programación Básica');
insert into cursos(id_curso,nombre) values(4,'Inglés');
insert into cursos(id_curso,nombre) values(5,'Electrónica Básica');
insert into cursos(id_curso,nombre) values(6,'Motor de Cuatro Tiempos');
insert into cursos(id_curso,nombre) values(7,'Enfermedades Laborales');
insert into cursos(id_curso,nombre) values(8,'Higiene Postural en el Trabajo');
insert into cursos(id_curso,nombre) values(9,'Ergonomía');
insert into cursos(id_curso,nombre) values(10,'Legislación Laboral en Colombia');
insert into cursos(id_curso,nombre) values(11,'Materiales de Soldadura');
insert into cursos(id_curso,nombre) values(12,'Métodos de Soldadura');
insert into cursos(id_curso,nombre) values(13,'Fusión de Metales');
insert into cursos(id_curso,nombre) values(14,'Buceo 1');
insert into cursos(id_curso,nombre) values(15,'Buceo 2');
insert into cursos(id_curso,nombre) values(16,'Riesgo Eléctrico');
insert into cursos(id_curso,nombre) values(17,'Bases de Datos Relacionales');
insert into cursos(id_curso,nombre) values(18,'Bases de Datos NO Relacionales');
insert into cursos(id_curso,nombre) values(19,'Electrónica Digital');
insert into cursos(id_curso,nombre) values(20,'Microprocesadores');

```
- Tabla curso_ruta
```sql
insert into curso_ruta(id_curso,id_ruta) values(1,1);
insert into curso_ruta(id_curso,id_ruta) values(2,1);
insert into curso_ruta(id_curso,id_ruta) values(3,1);
insert into curso_ruta(id_curso,id_ruta) values(6,3);
insert into curso_ruta(id_curso,id_ruta) values(17,3);
insert into curso_ruta(id_curso,id_ruta) values(18,3);
insert into curso_ruta(id_curso,id_ruta) values(4,4);
insert into curso_ruta(id_curso,id_ruta) values(5,5);
insert into curso_ruta(id_curso,id_ruta) values(11,5);
insert into curso_ruta(id_curso,id_ruta) values(12,5);
insert into curso_ruta(id_curso,id_ruta) values(13,5);
insert into curso_ruta(id_curso,id_ruta) values(19,5);
insert into curso_ruta(id_curso,id_ruta) values(20,5);
insert into curso_ruta(id_curso,id_ruta) values(7,9);
insert into curso_ruta(id_curso,id_ruta) values(8,9);
insert into curso_ruta(id_curso,id_ruta) values(9,9);
insert into curso_ruta(id_curso,id_ruta) values(16,9);
insert into curso_ruta(id_curso,id_ruta) values(10,10);
insert into curso_ruta(id_curso,id_ruta) values(14,11);
insert into curso_ruta(id_curso,id_ruta) values(15,11);

```

- Tabla instructores_curso_ruta
```sql
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (1, 1029384756, 3);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (2, 1029384756, 17);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (3, 1029384756, 20);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (9, 1123456789, 7);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (5, 1345678901, 5);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (6, 1567384920, 4);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (7, 1654327890, 19);
INSERT INTO proyecto_sena.instructores_curso_ruta (id_ruta, id_instructor, id_curso) VALUES (1, 1948273645, 18);

```

# Consultas.

1.	Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”

```sql
ALTER TABLE `matriculas`
ADD COLUMN `Estado_Matricula` ENUM('En Ejecución', 'Terminado', 'Cancelado') DEFAULT 'En Ejecución' AFTER `id_matricula`;

-- Update de la tabla matriculas.

UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 1;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 2;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 3;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 4;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'Terminado' WHERE id_matricula = 5;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 6;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 7;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'En Ejecución' WHERE id_matricula = 8;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'Terminado' WHERE id_matricula = 9;
UPDATE proyecto_sena.matriculas SET Estado_Matricula = 'Cancelado' WHERE id_matricula = 10;


```

2. Agregue a el campo edad a la tabla de Aprendices.

```sql
UPDATE `aprendices`
SET `edad` = 25  -- Nueva edad
WHERE `numero_documento` = 123123123;


    -- Update de la tabla aprendices
UPDATE proyecto_sena.aprendices SET edad = 20 WHERE numero_documento = 123123123;
UPDATE proyecto_sena.aprendices SET edad = 19 WHERE numero_documento = 123456789;
UPDATE proyecto_sena.aprendices SET edad = 21 WHERE numero_documento = 234567890;
UPDATE proyecto_sena.aprendices SET edad = 25 WHERE numero_documento = 345678901;
UPDATE proyecto_sena.aprendices SET edad = 32 WHERE numero_documento = 456789012;
UPDATE proyecto_sena.aprendices SET edad = 18 WHERE numero_documento = 567890123;
UPDATE proyecto_sena.aprendices SET edad = 45 WHERE numero_documento = 678901234;
UPDATE proyecto_sena.aprendices SET edad = 22 WHERE numero_documento = 789012345;
UPDATE proyecto_sena.aprendices SET edad = 26 WHERE numero_documento = 890123456;
UPDATE proyecto_sena.aprendices SET edad = 29 WHERE numero_documento = 901234567;

```
3.	Si suponemos que los cursos tienen una duración diferente dependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?

```sql
-- agregar un nuevo campo de duracion a cada curso dependiendo de la ruta especifica

ALTER TABLE `curso_ruta`
ADD COLUMN `duracion` INT DEFAULT 0 AFTER `id_ruta`;

-- La duracion se va a tomar en semanas para cada curso.
-- Update en la tabla  curso_ruta

UPDATE proyecto_sena.curso_ruta SET duracion = 12 WHERE id_curso = 1 AND id_ruta = 1;
UPDATE proyecto_sena.curso_ruta SET duracion = 10 WHERE id_curso = 2 AND id_ruta = 1;
UPDATE proyecto_sena.curso_ruta SET duracion = 8 WHERE id_curso = 3 AND id_ruta = 1;
UPDATE proyecto_sena.curso_ruta SET duracion = 12 WHERE id_curso = 4 AND id_ruta = 4;
UPDATE proyecto_sena.curso_ruta SET duracion = 8 WHERE id_curso = 5 AND id_ruta = 5;
UPDATE proyecto_sena.curso_ruta SET duracion = 16 WHERE id_curso = 6 AND id_ruta = 3;
UPDATE proyecto_sena.curso_ruta SET duracion = 6 WHERE id_curso = 7 AND id_ruta = 9;
UPDATE proyecto_sena.curso_ruta SET duracion = 8 WHERE id_curso = 8 AND id_ruta = 9;
UPDATE proyecto_sena.curso_ruta SET duracion = 10 WHERE id_curso = 9 AND id_ruta = 9;
UPDATE proyecto_sena.curso_ruta SET duracion = 8 WHERE id_curso = 10 AND id_ruta = 10;


```
4.	Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.
```sql
    SELECT a.nombre,edad
    FROM `aprendices` AS a
            JOIN carreras AS c ON a.id_carrera = c.id_carrera
    WHERE c.nombre = 'Electrónica';

```
### Resultado
```bash
+----------+------+
| nombre   | edad |
+----------+------+
| Andrea   |   21 |
| Santiago |   22 |
+----------+------+
```
5.	Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.

```sql

SELECT a.`nombre` AS 'Nombre del Aprendiz',
       r.`nombre` AS 'Ruta de Aprendizaje Cancelada'
FROM `aprendices` AS a
         INNER JOIN `rutas` AS r ON a.`id_carrera` = r.`id_carrera`
         INNER JOIN `matriculas` AS m ON a.`id_matricula` = m.`id_matricula`
WHERE m.`Estado_Matricula` = 'Cancelado';

```
### Resultado
```bash
+---------------------+--------------------------------+
| Nombre del Aprendiz | Ruta de Aprendizaje Cancelada  |
+---------------------+--------------------------------+
| Isabella            | Soldadura Autógena Industrial  |
| Isabella            | Soldadura Eléctrica Industrial |
| Isabella            | Soldadura Submarina            |
+---------------------+--------------------------------+
```
6.	Seleccionar Nombre de los cursos que no tienen un instructor asignado.

```sql
SELECT c.`nombre` AS 'Nombre del Curso'
FROM `cursos` AS c
        LEFT JOIN `instructores_curso_ruta` AS icr ON c.`id_curso` = icr.`id_curso`
WHERE icr.`id_curso` IS NULL;

```
### Resultado
```bash
+---------------------------------+
| Nombre del Curso                |
+---------------------------------+
| Matemáticas Básicas             |
| Álgebra Computacional           |
| Motor de Cuatro Tiempos         |
| Higiene Postural en el Trabajo  |
| Ergonomía                       |
| Legislación Laboral en Colombia |
| Materiales de Soldadura         |
| Métodos de Soldadura            |
| Fusión de Metales               |
| Buceo 1                         |
| Buceo 2                         |
| Riesgo Eléctrico                |
+---------------------------------+
```
7.	Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.

```sql
SELECT i.`nombre` AS 'Nombre del Instructor'
FROM `instructores` AS i
         INNER JOIN `instructores_curso_ruta` AS icr ON i.`numero_documento` = icr.`id_instructor`
         INNER JOIN `rutas` AS r ON icr.`id_ruta` = r.`id_ruta`
WHERE r.`nombre` = 'Sistemas de Información Empresariales';
```
### Resultado
```bash
+------------------------+
| Nombre del Instructor  |
+------------------------+
| Ricardo Vicente Jaimes |
| Andrea González        |
+------------------------+
```
8.	Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje)

```sql
SELECT a.`nombre` AS 'Nombre del Aprendiz',
       c.`nombre` AS 'Nombre de la Carrera',
       r.`nombre` AS 'Énfasis de la Carrera (Ruta de Aprendizaje)'
FROM `aprendices` AS a
         INNER JOIN `carreras` AS c ON a.`id_carrera` = c.`id_carrera`
         INNER JOIN `rutas` AS r ON a.`id_carrera` = r.`id_carrera`
         INNER JOIN `matriculas` AS m ON a.`id_matricula` = m.`id_matricula`
WHERE m.`Estado_Matricula` = 'Terminado';
```
### Resultado
```bash
+---------------------+-------------------------------+----------------------------------------------+
| Nombre del Aprendiz | Nombre de la Carrera          | Énfasis de la Carrera (Ruta de Aprendizaje)  |
+---------------------+-------------------------------+----------------------------------------------+
| Diego               | Soldadura                     | Soldadura Autógena Industrial                |
| Diego               | Soldadura                     | Soldadura Eléctrica Industrial               |
| Diego               | Soldadura                     | Soldadura Submarina                          |
| Alejandro           | Seguridad y Salud Ocupacional | Sistemas de Gestión en Seguridad Ocupacional |
+---------------------+-------------------------------+----------------------------------------------+
```

10.	Nombres de Instructores que no tienen curso asignado
```sql
SELECT i.`nombre` AS 'Nombre del Instructor'
FROM `instructores` AS i
         LEFT JOIN `instructores_curso_ruta` AS icr ON i.`numero_documento` = icr.`id_instructor`
WHERE icr.`id_instructor` IS NULL;
```
### Resultado
```bash
+------------------------+
| Nombre del Instructor  |
+------------------------+
| Agustín Parra Granados |
| Juan Carlos Cobos      |
| Pedro Nell Santoamaría |
| Marisela Sevilla       |
+------------------------+
```

# Preguntas de tipo seleccion multiple.

1.