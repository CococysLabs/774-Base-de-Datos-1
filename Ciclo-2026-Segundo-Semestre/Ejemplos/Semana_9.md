
# Semana 9 - Funciones de Grupo en Oracle

En esta semana aprenderemos a utilizar funciones de grupo en Oracle SQL para realizar cálculos sobre los registros de una tabla. También veremos cómo agrupar información, filtrar resultados agrupados y trabajar con valores nulos.

### Creación de la tabla

- Creamos una tabla llamada Ventas para almacenar información de diferentes ventas.
- La tabla contiene un identificador, el nombre del vendedor, la categoría del producto y el monto vendido.
- Utilizamos PRIMARY KEY para identificar de manera única cada venta.

```sql
CREATE TABLE Ventas (
    id_venta NUMBER PRIMARY KEY,
    vendedor VARCHAR2(50),
    categoria VARCHAR2(30),
    monto NUMBER(10,2)
);
```

### Inserción de registros

- Utilizamos INSERT INTO para agregar información a nuestra tabla.
- Insertamos seis ventas realizadas por diferentes vendedores.
- Incluimos un valor NULL para observar cómo se comportan las funciones de grupo cuando existen datos nulos.

```sql
INSERT INTO Ventas VALUES (1, 'Carlos', 'Tecnologia', 1500);
INSERT INTO Ventas VALUES (2, 'Ana', 'Ropa', 500);
INSERT INTO Ventas VALUES (3, 'Carlos', 'Tecnologia', 2000);
INSERT INTO Ventas VALUES (4, 'Maria', 'Ropa', 800);
INSERT INTO Ventas VALUES (5, 'Ana', 'Tecnologia', 1200);
INSERT INTO Ventas VALUES (6, 'Maria', 'Ropa', NULL);
```

### Consulta inicial

- SELECT permite consultar los registros almacenados en nuestra tabla.
- Utilizamos * para mostrar todas las columnas.

```sql
SELECT * FROM Ventas;
```

### Funciones de grupo

- Las funciones de grupo permiten realizar operaciones sobre varios registros.
- COUNT cuenta registros o valores no nulos.
- SUM calcula la suma de los valores.
- AVG calcula el promedio.
- MIN obtiene el valor mínimo.
- MAX obtiene el valor máximo.

En esta consulta contamos cuántas ventas existen en nuestra tabla.

```sql
SELECT COUNT(*) AS total_ventas
FROM Ventas;
```

Ahora calculamos el total vendido y el promedio de los montos registrados.

```sql
SELECT
    SUM(monto) AS total_vendido,
    AVG(monto) AS promedio_ventas
FROM Ventas;
```

También podemos obtener la venta más pequeña y la más grande.

```sql
SELECT
    MIN(monto) AS venta_minima,
    MAX(monto) AS venta_maxima
FROM Ventas;
```

### Uso de COUNT y valores NULL

- COUNT(*) cuenta todas las filas de la tabla.
- COUNT(columna) cuenta únicamente los valores que no son NULL.
- Las funciones SUM y AVG también ignoran los valores NULL.

En este ejemplo comparamos la cantidad total de ventas con la cantidad de ventas que tienen un monto registrado.

```sql
SELECT
    COUNT(*) AS total_registros,
    COUNT(monto) AS montos_registrados
FROM Ventas;
```

### Uso de DISTINCT

- DISTINCT permite obtener valores sin repetirlos.
- Podemos utilizarlo para identificar los vendedores diferentes que aparecen en nuestra tabla.
- También podemos combinar DISTINCT con COUNT para contar valores únicos.

En este ejemplo mostramos los nombres de los vendedores sin duplicados.

```sql
SELECT DISTINCT vendedor
FROM Ventas;
```

Ahora contamos cuántos vendedores diferentes existen.

```sql
SELECT COUNT(DISTINCT vendedor) AS total_vendedores
FROM Ventas;
```

### Uso de NVL

- NVL permite reemplazar un valor NULL por otro valor.
- Podemos utilizar NVL(monto, 0) para mostrar un cero cuando el monto no tenga información.
- Esto facilita la presentación de resultados y permite controlar cómo se realizan algunos cálculos.

En esta consulta mostramos las ventas reemplazando los montos nulos por cero.

```sql
SELECT
    vendedor,
    categoria,
    NVL(monto, 0) AS monto
FROM Ventas;
```

### Agrupación de resultados con GROUP BY

- GROUP BY permite agrupar registros que contienen valores iguales.
- Podemos combinarlo con funciones como SUM, COUNT y AVG.
- Es útil para generar reportes por vendedor, categoría o departamento.

En este ejemplo calculamos el total vendido por cada vendedor.

```sql
SELECT
    vendedor,
    SUM(monto) AS total_vendido
FROM Ventas
GROUP BY vendedor;
```

También podemos contar cuántas ventas realizó cada vendedor.

```sql
SELECT
    vendedor,
    COUNT(*) AS cantidad_ventas
FROM Ventas
GROUP BY vendedor;
```

### Filtrado de grupos con HAVING

- HAVING permite filtrar los resultados después de realizar una agrupación.
- WHERE filtra registros individuales antes de agruparlos.
- HAVING se utiliza cuando necesitamos aplicar condiciones sobre resultados de funciones de grupo.

En este ejemplo mostramos únicamente los vendedores cuyo total de ventas es mayor a 2000.

```sql
SELECT
    vendedor,
    SUM(monto) AS total_vendido
FROM Ventas
GROUP BY vendedor
HAVING SUM(monto) > 2000;
```

### Ordenamiento de resultados

- ORDER BY permite ordenar los resultados de nuestras consultas.
- DESC ordena de mayor a menor.
- Podemos utilizar ORDER BY junto con GROUP BY para organizar nuestros reportes.

En este ejemplo mostramos el total vendido por cada categoría, comenzando por la categoría con mayores ventas.

```sql
SELECT
    categoria,
    SUM(monto) AS total_vendido
FROM Ventas
GROUP BY categoria
ORDER BY total_vendido DESC;
```

### Conclusión

Durante esta semana aprendimos a utilizar funciones de grupo en Oracle SQL para analizar la información almacenada en una tabla.

- Utilizamos COUNT para contar registros.
- Aplicamos SUM y AVG para calcular totales y promedios.
- Utilizamos MIN y MAX para obtener valores mínimos y máximos.
- Aprendimos a trabajar con valores NULL y la función NVL.
- Utilizamos DISTINCT para evitar resultados duplicados.
- Agrupamos registros mediante GROUP BY.
- Filtramos resultados agrupados utilizando HAVING.
- Ordenamos los resultados con ORDER BY.

Estos conocimientos nos permiten generar reportes y obtener información resumida de una base de datos de manera más sencilla y organizada.
