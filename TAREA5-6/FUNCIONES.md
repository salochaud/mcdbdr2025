# Tarea 5-6
## Creacion de Datos Ficticios y Funciones

Se trabajo con la herramienta FillDB permite generar datos ficticios de manera rápida.

### Conteo de frecuencias

```mysql
SELECT AVG(total) AS promedio_venta
FROM ventas;
```
### Mínimos o máximos
```mysql
SELECT MIN(total) AS venta_minima, MAX(total) AS venta_maxima
FROM ventas;
```
### Cuantil 
```mysql
SELECT PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY total) AS percentil_25
FROM ventas;
``` 
### Moda
```mysql
SELECT total, COUNT(*) AS frecuencia
FROM ventas
GROUP BY total
ORDER BY frecuencia DESC
LIMIT 1;
```

### Hallazgos

- El promedio de venta es razonable para una tienda digital.

- Existencia de valores atípicos,algunas ventas registradas con totales muy altos (> $40) podrían indicar la compra de ediciones especiales o bundles de videojuegos.

- Compras concentradas por cliente, al hacer un GROUP BY id_cliente, se observó que ciertos clientes realizan varias compras, lo cual es útil para estrategias de fidelización o programa de recompensas.

- Picos de compra en ciertas fechas, al agrupar por fecha_venta, se observan acumulaciones en ciertos días (posibles fines de semana o lanzamientos), lo que podría indicar patrones de comportamiento de compra.

- El cuantil 25% indica que una parte de los clientes compra juegos muy baratos.

### Dificultades

- PERCENTILE_CONT solo está disponible en MySQL 8.0+ o PostgreSQL.

- No hay función directa para moda en SQL: se resolvió con GROUP BY + ORDER BY COUNT(*) DESC.

- FillDB no respeta relaciones entre tablas (como claves foráneas).

### Soluciones

- Se usó FillDB con campos personalizados como -- float(5,50) para el campo total.

- Se usó AUTO_INCREMENT para evitar errores de duplicados en IDs.

- Se generaron primero las tablas base y luego las relacionadas.




