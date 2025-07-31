# Tarea 9 

# Procedimientos   

 ### Cantidad de elementos de un arreglo
 ¿Que hace? Calcula cuántos productos fueron vendidos por cada venta.
 ```sql
 DELIMITER //

CREATE FUNCTION contar_productos_por_venta(ventaId INT)
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE total INT;
    SELECT COUNT(*) INTO total
    FROM detalle_venta
    WHERE id_venta = ventaId;
    RETURN total;
END //

DELIMITER ;
```

### Simulación de correlación entre cantidad y total
 ```sql
-- Media de cantidad y total
SELECT 
    AVG(cantidad) AS media_cantidad,
    AVG(total) AS media_total
FROM detalle_venta;

-- Luego se podría simular una correlación con subconsultas o exportar a herramientas externas como Python.
 ```
### Distancia de Levenshtein entre dos nombres de clientes
 ```sql
 DELIMITER //

CREATE FUNCTION levenshtein(s1 VARCHAR(255), s2 VARCHAR(255))
RETURNS INT
DETERMINISTIC
BEGIN
  DECLARE s1_len, s2_len, i, j, c, c_temp, cost INT;
  DECLARE s1_char CHAR;
  DECLARE cv0, cv1 TEXT;

  SET s1_len = CHAR_LENGTH(s1), s2_len = CHAR_LENGTH(s2), cv1 = '', j = 1;

  WHILE j <= s2_len DO
    SET cv1 = CONCAT(cv1, CHAR(j));
    SET j = j + 1;
  END WHILE;

  SET i = 1;

  WHILE i <= s1_len DO
    SET s1_char = SUBSTRING(s1, i, 1), c = i, cv0 = CHAR(i), j = 1;

    WHILE j <= s2_len DO
      SET c = c + 1;
      SET cost = IF(s1_char = SUBSTRING(s2, j, 1), 0, 1);
      SET c_temp = ASCII(SUBSTRING(cv1, j, 1)) + cost;
      IF ASCII(SUBSTRING(cv0, j, 1)) + 1 < c_temp THEN SET c_temp = ASCII(SUBSTRING(cv0, j, 1)) + 1; END IF;
      IF j > 1 AND ASCII(SUBSTRING(cv1, j - 1, 1)) + 1 < c_temp THEN SET c_temp = ASCII(SUBSTRING(cv1, j - 1, 1)) + 1; END IF;
      SET cv0 = INSERT(cv0, j, 1, CHAR(c_temp));
      SET j = j + 1;
    END WHILE;

    SET cv1 = cv0;
    SET i = i + 1;
  END WHILE;

  RETURN ASCII(SUBSTRING(cv1, s2_len, 1));
END //

DELIMITER ;
 ```
 ### Explicación de tarea
En esta tarea se implementaron funciones avanzadas usando SQL sobre la base de datos ventas. Se creó una función que cuenta cuántos productos se venden por cada ticket (venta), útil para conocer el tamaño promedio de compras.

También se intentó simular una correlación entre la cantidad de productos y el total de venta.

Se creó una función para calcular la distancia de Levenshtein entre nombres de clientes, lo cual puede ayudar en procesos de limpieza de datos.

Estas funciones permiten extender el análisis estadístico y de calidad de datos directamente en SQL, mejorando la preparación de datos para su explotación futura.
