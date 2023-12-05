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
