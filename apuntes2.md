# Ejercicios Avanzados de SQL 2

Este documento proporciona una serie de ejercicios avanzados para ayudarte a mejorar tus habilidades en SQL. Cada ejercicio incluye una descripción y el código SQL necesario para completarlo.

## Configuración Inicial

### 1. Crear una Base de Datos
Para comenzar, necesitamos crear una base de datos llamada `escuela`. Esto se hace con el siguiente comando:
```sql
CREATE DATABASE escuela;
USE escuela;
2. Crear Tablas
Vamos a crear tres tablas: estudiantes, cursos e inscripciones. Estas tablas almacenarán información sobre los estudiantes, los cursos y las inscripciones respectivamente.

Tabla estudiantes

CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT,
    grado VARCHAR(10)
);
Esta tabla contiene información sobre los estudiantes, incluyendo un ID único, nombre, edad y grado.

Tabla cursos

CREATE TABLE cursos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    descripcion TEXT
);
Esta tabla contiene información sobre los cursos, incluyendo un ID único, nombre y descripción.

Tabla inscripciones

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

INSERT INTO estudiantes (nombre, edad, grado) VALUES
('Juan Pérez', 15, '10'),
('María García', 14, '9'),
('Pedro Martínez', 16, '11'),
('Ana López', 17, '12'),
('Carlos Ruiz', 18, '12');
Insertar Datos en cursos

INSERT INTO cursos (nombre, descripcion) VALUES
('Matemáticas', 'Curso de matemáticas avanzadas'),
('Ciencias', 'Curso de ciencias naturales'),
('Historia', 'Curso de historia mundial'),
('Física', 'Curso de física teórica'),
('Química', 'Curso de química orgánica');
Insertar Datos en inscripciones

INSERT INTO inscripciones (estudiante_id, curso_id, fecha_inscripcion) VALUES
(1, 1, '2023-09-01'),
(1, 2, '2023-09-02'),
(2, 3, '2023-09-01'),
(3, 4, '2023-09-03'),
(4, 5, '2023-09-04'),
(5, 1, '2023-09-05'),
(5, 3, '2023-09-06');
Ejercicios
1. Seleccionar Estudiantes Inscritos en Más de un Curso
Descripción: Selecciona los estudiantes que están inscritos en más de un curso.


SELECT estudiante_id, COUNT(*) AS numero_de_cursos
FROM inscripciones
GROUP BY estudiante_id
HAVING COUNT(*) > 1;
Este comando muestra los estudiantes que están inscritos en más de un curso.

2. Encontrar el Curso con Más Inscripciones
Descripción: Selecciona el curso que tiene el mayor número de inscripciones.


SELECT curso_id, COUNT(*) AS numero_de_inscripciones
FROM inscripciones
GROUP BY curso_id
ORDER BY numero_de_inscripciones DESC
LIMIT 1;
Este comando muestra el curso con el mayor número de inscripciones.

3. Calcular la Edad Promedio de los Estudiantes por Grado
Descripción: Calcula la edad promedio de los estudiantes en cada grado.


SELECT grado, AVG(edad) AS edad_promedio
FROM estudiantes
GROUP BY grado;
Este comando muestra la edad promedio de los estudiantes para cada grado.

4. Seleccionar Estudiantes y el Número de Cursos en los que Están Inscritos
Descripción: Selecciona los nombres de los estudiantes y el número de cursos en los que están inscritos.


SELECT estudiantes.nombre, COUNT(inscripciones.curso_id) AS numero_de_cursos
FROM estudiantes
LEFT JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id
GROUP BY estudiantes.id;
Este comando muestra los nombres de los estudiantes junto con el número de cursos en los que están inscritos.

5. Encontrar Estudiantes Inscritos en el Curso de Matemáticas
Descripción: Selecciona los nombres de los estudiantes que están inscritos en el curso de Matemáticas.

SELECT estudiantes.nombre
FROM estudiantes
JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id
JOIN cursos ON inscripciones.curso_id = cursos.id
WHERE cursos.nombre = 'Matemáticas';
Este comando muestra los nombres de los estudiantes inscritos en el curso de Matemáticas.

6. Determinar el Número de Inscripciones por Mes
Descripción: Cuenta el número de inscripciones para cada mes del año 2023.


SELECT MONTH(fecha_inscripcion) AS mes, COUNT(*) AS numero_de_inscripciones
FROM inscripciones
WHERE YEAR(fecha_inscripcion) = 2023
GROUP BY MONTH(fecha_inscripcion);
Este comando muestra el número de inscripciones por cada mes del año 2023.

7. Encontrar los Estudiantes que No Están Inscritos en Ningún Curso
Descripción: Selecciona los nombres de los estudiantes que no están inscritos en ningún curso.


SELECT nombre
FROM estudiantes
WHERE id NOT IN (SELECT estudiante_id FROM inscripciones);
Este comando muestra los nombres de los estudiantes que no están inscritos en ningún curso.

8. Encontrar el Curso con la Descripción Más Larga
Descripción: Selecciona el nombre del curso con la descripción más larga.


SELECT nombre
FROM cursos
ORDER BY LENGTH(descripcion) DESC
LIMIT 1;
Este comando muestra el nombre del curso con la descripción más larga.

9. Unir Tablas para Mostrar el Número de Inscripciones por Curso y Grado
Descripción: Muestra el número de inscripciones por curso y grado.


SELECT cursos.nombre AS nombre_del_curso, estudiantes.grado, COUNT(*) AS numero_de_inscripciones
FROM inscripciones
JOIN estudiantes ON inscripciones.estudiante_id = estudiantes.id
JOIN cursos ON inscripciones.curso_id = cursos.id
GROUP BY cursos.nombre, estudiantes.grado;
Este comando une las tablas y muestra el número de inscripciones por curso y grado.

10. Actualizar el Grado de los Estudiantes que Cumplieron Años
Descripción: Actualiza el grado de los estudiantes que cumplieron años este año y pasaron al siguiente grado.


UPDATE estudiantes
SET grado = CASE 
    WHEN grado = '9' THEN '10'
    WHEN grado = '10' THEN '11'
    WHEN grado = '11' THEN '12'
    WHEN grado = '12' THEN 'Graduado'
    ELSE grado
END
WHERE id IN (SELECT estudiante_id FROM inscripciones WHERE YEAR(fecha_inscripcion) = YEAR(CUR
