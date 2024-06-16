# Ejercicios Prácticos de SQL

Este documento proporciona una serie de ejercicios prácticos para ayudarte a aprender y practicar SQL. Cada ejercicio incluye una descripción y el código SQL necesario para completarlo.

## Configuración Inicial

### 1. Crear una Base de Datos
Para comenzar, necesitamos crear una base de datos llamada `escuela`. Esto se hace con el siguiente comando:
```sql
CREATE DATABASE escuela;
USE escuela;
Crear Tablas
Vamos a crear tres tablas: estudiantes, cursos e inscripciones. Estas tablas almacenarán información sobre los estudiantes, los cursos y las inscripciones respectivamente.

Tabla estudiantes
sql
Copiar código
CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT,
    grado VARCHAR(10)
);
Esta tabla contiene información sobre los estudiantes, incluyendo un ID único, nombre, edad y grado.

Tabla cursos
sql
Copiar código
CREATE TABLE cursos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    descripcion TEXT
);
Esta tabla contiene información sobre los cursos, incluyendo un ID único, nombre y descripción.

Tabla inscripciones
sql
Copiar código
CREATE TABLE inscripciones (
    id INT AUTO_INCREMENT PRIMARY KEY,
    estudiante_id INT,
    curso_id INT,
    fecha_inscripcion DATE,
    FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id),
    FOREIGN KEY (curso_id) REFERENCES cursos(id)
);
Esta tabla almacena las inscripciones de los estudiantes en los cursos, incluyendo un ID único, el ID del estudiante, el ID del curso y la fecha de inscripción. Las claves foráneas aseguran que los estudiante_id y curso_id existan en las tablas estudiantes y cursos respectivamente.

3. Insertar Datos
Vamos a insertar algunos datos iniciales en nuestras tablas.

Insertar Datos en estudiantes
sql
Copiar código
INSERT INTO estudiantes (nombre, edad, grado) VALUES
('Juan Pérez', 15, '10'),
('María García', 14, '9'),
('Pedro Martínez', 16, '11');
Insertar Datos en cursos
sql
Copiar código
INSERT INTO cursos (nombre, descripcion) VALUES
('Matemáticas', 'Curso de matemáticas avanzadas'),
('Ciencias', 'Curso de ciencias naturales'),
('Historia', 'Curso de historia mundial');
Insertar Datos en inscripciones
sql
Copiar código
INSERT INTO inscripciones (estudiante_id, curso_id, fecha_inscripcion) VALUES
(1, 1, '2023-09-01'),
(1, 2, '2023-09-02'),
(2, 3, '2023-09-01');
Ejercicios
1. Seleccionar Todos los Estudiantes
Descripción: Selecciona todos los estudiantes de la tabla estudiantes.

sql
Copiar código
SELECT * FROM estudiantes;
Este comando muestra todos los registros de la tabla estudiantes.

2. Seleccionar Nombres y Edades de los Estudiantes
Descripción: Selecciona solo los nombres y las edades de los estudiantes.

sql
Copiar código
SELECT nombre, edad FROM estudiantes;
Este comando muestra solo las columnas nombre y edad de la tabla estudiantes.

3. Encontrar Estudiantes en un Grado Específico
Descripción: Selecciona los estudiantes que están en el grado '10'.

sql
Copiar código
SELECT * FROM estudiantes WHERE grado = '10';
Este comando muestra los estudiantes que están en el grado 10.

4. Ordenar Estudiantes por Edad
Descripción: Selecciona todos los estudiantes y ordénalos por edad de manera ascendente.

sql
Copiar código
SELECT * FROM estudiantes ORDER BY edad ASC;
Este comando muestra todos los estudiantes ordenados por su edad en orden ascendente.

5. Contar el Número de Estudiantes
Descripción: Cuenta cuántos estudiantes hay en la tabla estudiantes.

sql
Copiar código
SELECT COUNT(*) AS total_estudiantes FROM estudiantes;
Este comando cuenta el número total de estudiantes en la tabla estudiantes.

6. Seleccionar Estudiantes con Edades Entre 15 y 16
Descripción: Selecciona los estudiantes cuya edad está entre 15 y 16 años.

sql
Copiar código
SELECT * FROM estudiantes WHERE edad BETWEEN 15 AND 16;
Este comando muestra los estudiantes cuya edad está entre 15 y 16 años.

7. Encontrar Inscripciones de un Estudiante
Descripción: Selecciona todas las inscripciones del estudiante con id = 1.

sql
Copiar código
SELECT * FROM inscripciones WHERE estudiante_id = 1;
Este comando muestra todas las inscripciones del estudiante con ID 1.

8. Unir Tablas de Estudiantes e Inscripciones
Descripción: Realiza una unión entre las tablas estudiantes e inscripciones para mostrar el nombre del estudiante y la fecha de inscripción.

sql
Copiar código
SELECT estudiantes.nombre, inscripciones.fecha_inscripcion
FROM estudiantes
JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id;
Este comando une las tablas estudiantes e inscripciones y muestra el nombre del estudiante junto con la fecha de inscripción.

9. Unir Tablas de Inscripciones y Cursos
Descripción: Realiza una unión entre las tablas inscripciones y cursos para mostrar el nombre del curso y la fecha de inscripción.

sql
Copiar código
SELECT cursos.nombre, inscripciones.fecha_inscripcion
FROM inscripciones
JOIN cursos ON inscripciones.curso_id = cursos.id;
Este comando une las tablas inscripciones y cursos y muestra el nombre del curso junto con la fecha de inscripción.

10. Agregar un Nuevo Estudiante
Descripción: Agrega un nuevo estudiante a la tabla estudiantes.

sql
Copiar código
INSERT INTO estudiantes (nombre, edad, grado) VALUES ('Ana López', 17, '12');
Este comando agrega un nuevo estudiante llamado Ana López a la tabla estudiantes.

11. Actualizar la Edad de un Estudiante
Descripción: Actualiza la edad del estudiante con id = 2 a 15 años.

sql
Copiar código
UPDATE estudiantes SET edad = 15 WHERE id = 2;
Este comando actualiza la edad del estudiante con ID 2 a 15 años.

12. Eliminar una Inscripción
Descripción: Elimina la inscripción con id = 3.

sql
Copiar código
DELETE FROM inscripciones WHERE id = 3;
