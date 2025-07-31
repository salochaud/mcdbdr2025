# Tarea 8

## Tarea 8 – Vistas y Disparadores en SQL  


### Vista con JOIN

```sql
CREATE VIEW vista_ventas_detalladas AS
SELECT ventas.id_venta, clientes.nombre AS nombre_cliente, videojuegos.nombre AS nombre_juego, ventas.fecha_venta, ventas.total
FROM ventas
JOIN clientes ON ventas.id_cliente = clientes.id_cliente
JOIN videojuegos ON ventas.id_videojuego = videojuegos.id_videojuego;
```
Esta vista combina los datos de la tabla ventas con los nombres de clientes y videojuegos, permitiendo consultar todas las ventas con contexto completo.

### Vista con LEFT JOIN
```sql
CREATE VIEW vista_clientes_y_ventas AS
SELECT clientes.id_cliente, clientes.nombre, ventas.id_venta, ventas.total
FROM clientes
LEFT JOIN ventas ON clientes.id_cliente = ventas.id_cliente;
```
Incluye a todos los clientes, incluso los que no han realizado ninguna compra (usando LEFT JOIN).

### Vista con RIGHT JOIN
 ```sql
CREATE VIEW vista_juegos_y_ventas AS
SELECT videojuegos.id_videojuego, videojuegos.nombre, ventas.id_venta, ventas.total
FROM ventas
RIGHT JOIN videojuegos ON ventas.id_videojuego = videojuegos.id_videojuego;
```
Muestra todos los videojuegos, incluso los que nunca se han vendido 

### Vista con subconsulta
 ```sql
CREATE VIEW vista_top_clientes AS
SELECT id_cliente, total_gastado FROM (
    SELECT id_cliente, SUM(total) AS total_gastado
    FROM ventas
    GROUP BY id_cliente
) AS resumen
WHERE total_gastado > 100;
 ```

 Muestra solo los clientes cuyo gasto total acumulado supera los 100 unidades monetarias.

### Creación de un trigger
 ```sql
DELIMITER $$

CREATE TRIGGER after_venta_insert
AFTER INSERT ON ventas
FOR EACH ROW
BEGIN
  INSERT INTO log_ventas (id_venta, mensaje, fecha_registro)
  VALUES (NEW.id_venta, CONCAT('Venta registrada por cliente ', NEW.id_cliente), NOW());
END$$

DELIMITER ;
 ```
 Cada vez que se inserta una nueva venta, este trigger guarda un registro en la tabla log_ventas con un mensaje y la fecha. Útil para auditoría o debugging.

### Beneficios de las vistas
- Abstracción: Facilitan el acceso a consultas complejas como si fueran tablas.

- Reutilización: Se pueden usar en otras consultas sin reescribir JOINs o GROUP BY.

- Seguridad: Pueden mostrar solo columnas específicas a ciertos usuarios.

### Beneficios del trigger:
- Auditoría: Automatiza el registro de acciones sin requerir código externo.

- Automatización: Puedes disparar acciones de forma automática.

- Consistencia: Garantiza que ciertas tareas se ejecuten siempre que ocurra un evento.