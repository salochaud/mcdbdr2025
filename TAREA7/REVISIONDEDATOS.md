# Tarea 7
## Revision de datos 

## Inconsistencias

Durante el análisis de la tabla `ventas` generada con FillDB, se detectaron las siguientes inconsistencias:

- Algunos registros tienen valores `total` menores a $5 o superiores a $50, lo cual se sale del rango lógico esperado para videojuegos individuales.
- Hay registros con el mismo `id_venta` (esto ocurre si no se usó `AUTO_INCREMENT` correctamente).
- Algunos valores en `id_cliente` o `id_videojuego` no corresponden con ninguna entrada real en sus respectivas tablas (clientes o productos no existen).
- Se detectaron fechas fuera del rango esperado (ventas en años pasados o futuros).


## Modificaciones 

Para resolver las inconsistencias mencionadas, se realizaron los siguientes ajustes:

```sql
-- Asegurar que id_venta sea clave única con incremento automático
ALTER TABLE ventas MODIFY id_venta INT AUTO_INCREMENT PRIMARY KEY;

-- Eliminar registros con total fuera de rango esperado
DELETE FROM ventas
WHERE total < 5 OR total > 50;

-- Eliminar registros con fechas futuras
DELETE FROM ventas
WHERE fecha_venta > CURDATE();

-- Establecer valores válidos en claves foráneas
UPDATE ventas
SET id_cliente = 1
WHERE id_cliente NOT IN (SELECT id_cliente FROM clientes);

UPDATE ventas
SET id_videojuego = 1
WHERE id_videojuego NOT IN (SELECT id_videojuego FROM videojuegos);
```

## Subconsultas 

¿Qué cliente ha gastado más dinero en total?

```sql
SELECT id_cliente, total_gastado FROM (
    SELECT id_cliente, SUM(total) AS total_gastado
    FROM ventas
    GROUP BY id_cliente
) AS resumen
ORDER BY total_gastado DESC
LIMIT 1;
```
¿Qué videojuegos tienen un precio por venta superior al promedio?
```sql
SELECT *
FROM ventas
WHERE total > (
    SELECT AVG(total) FROM ventas
);
```
¿Cuál es el videojuego más vendido en número de transacciones?
```sql
SELECT id_videojuego, total_ventas FROM (
    SELECT id_videojuego, COUNT(*) AS total_ventas
    FROM ventas
    GROUP BY id_videojuego
) AS sub
ORDER BY total_ventas DESC
LIMIT 1;
```
## Hallazgos
- Se eliminaron registros inconsistentes que dificultaban el análisis estadístico.

- Se reforzaron claves primarias con AUTO_INCREMENT para evitar duplicados.

- Las subconsultas facilitaron la identificación de los clientes más activos y productos más vendidos.

- El uso de subconsultas anidadas permite realizar análisis más profundos sin necesidad de crear vistas.
