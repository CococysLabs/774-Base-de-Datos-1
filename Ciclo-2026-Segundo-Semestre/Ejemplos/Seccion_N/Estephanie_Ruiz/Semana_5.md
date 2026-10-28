

# Semana 5 - Consultas SQL en Oracle

En esta semana aprenderemos a realizar consultas SQL utilizando diferentes operadores, concatenaciones y ordenamientos. También veremos cómo insertar, actualizar y eliminar registros de una tabla.

### Creación de la tabla

- Creamos una tabla llamada Estudiantes para almacenar información básica de los estudiantes.
- La tabla contiene un identificador, nombre, apellido, nota final y fecha de inscripción.
- Utilizamos PRIMARY KEY para identificar de manera única a cada estudiante.

```sql
CREATE TABLE Estudiantes (
    id_estudiante NUMBER PRIMARY KEY,
    nombre VARCHAR2(50),
    apellido VARCHAR2(50),
    nota_final NUMBER(5,2),
    fecha_inscripcion DATE
);
```

### Inserción de registros

- Utilizamos INSERT INTO para agregar información a nuestra tabla.
- Insertamos tres estudiantes con diferentes nombres, apellidos y notas.
- TO_DATE permite convertir un texto en una fecha reconocida por Oracle.

```sql
INSERT INTO Estudiantes VALUES (1, 'Paulo', 'Argueta', 85.50, TO_DATE('2024-02-01', 'YYYY-MM-DD'));

INSERT INTO Estudiantes VALUES (2, 'Estephanie', 'Ruiz', 92.00, TO_DATE('2024-02-15', 'YYYY-MM-DD'));

INSERT INTO Estudiantes VALUES (3, 'Carlos', 'Gomez', 58.00, TO_DATE('2024-01-20', 'YYYY-MM-DD'));
```

### Consultas con WHERE, AND y OR

- WHERE permite filtrar los registros de acuerdo con una condición.
- AND requiere que ambas condiciones se cumplan.
- OR permite obtener registros cuando al menos una condición se cumple.
- NOT permite negar una condición.

En la primera consulta buscamos estudiantes que tengan una nota mayor o igual a 61 y cuyo apellido sea Argueta.

```sql
SELECT * FROM Estudiantes
WHERE nota_final >= 61 AND apellido = 'Argueta';
```

En la segunda consulta buscamos estudiantes con nota menor a 61 o cuyo nombre no sea Paulo.

```sql
SELECT nombre, nota_final
FROM Estudiantes
WHERE nota_final < 61 OR NOT nombre = 'Paulo';
```

### Concatenación de cadenas

- En Oracle utilizamos el operador || para unir textos.
- Podemos concatenar columnas de una tabla o agregar texto personalizado.
- AS permite asignar un nombre diferente a una columna en el resultado.

En este ejemplo unimos el nombre y el apellido en una sola columna llamada Nombre Completo.

```sql
SELECT nombre || ' ' || apellido AS "Nombre Completo", nota_final
FROM Estudiantes;
```

También podemos combinar texto con los valores almacenados en la tabla para generar un pequeño reporte.

```sql
SELECT 'El estudiante ' || nombre || ' tiene una nota de: ' || nota_final AS "Reporte"
FROM Estudiantes;
```

### Ordenamiento de resultados

- ORDER BY permite ordenar los registros obtenidos de una consulta.
- ASC ordena de manera ascendente, de menor a mayor o alfabéticamente.
- DESC ordena de manera descendente, de mayor a menor.

En esta consulta mostramos los estudiantes ordenados según su nota, comenzando por la más alta.

```sql
SELECT * FROM Estudiantes
ORDER BY nota_final DESC;
```

En este ejemplo ordenamos los estudiantes alfabéticamente por apellido.

```sql
SELECT * FROM Estudiantes
ORDER BY apellido ASC;
```

### Actualización de registros

- UPDATE permite modificar información existente en una tabla.
- SET indica qué columna queremos modificar.
- WHERE determina qué registros serán actualizados.

En este ejemplo aumentamos 5 puntos a la nota de Carlos por participación.

```sql
UPDATE Estudiantes
SET nota_final = nota_final + 5
WHERE nombre = 'Carlos';
```

### Eliminación de registros

- DELETE permite eliminar registros de una tabla.
- WHERE indica qué registro deseamos eliminar.
- Es importante utilizar WHERE para evitar eliminar todos los registros accidentalmente.

En este ejemplo eliminamos al estudiante cuyo identificador es 2.

```sql
DELETE FROM Estudiantes
WHERE id_estudiante = 2;
```

### Conclusión

Durante esta semana aprendimos a utilizar diferentes instrucciones SQL para consultar y manipular información almacenada en una base de datos Oracle.

- Utilizamos SELECT y WHERE para consultar información.
- Aplicamos AND, OR y NOT para combinar condiciones.
- Utilizamos || para concatenar cadenas de texto.
- Ordenamos resultados mediante ORDER BY, ASC y DESC.
- Modificamos registros utilizando UPDATE.
- Eliminamos registros utilizando DELETE.

Estos conocimientos permiten realizar consultas más específicas y trabajar con los datos de una manera más organizada.
