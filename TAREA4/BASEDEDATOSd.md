# Tarea 4
## Creacion de Tablas 

```mysql

CREATE DATABASE tienda_videojuegos;
USE tienda_videojuegos;

CREATE TABLE CLIENTE (
    cliente_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_usuario VARCHAR(100),
    correo VARCHAR(100),
    pais VARCHAR(50)
);

CREATE TABLE VIDEOJUEGO (
    videojuego_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(255),
    desarrollador VARCHAR(100),
    publisher VARCHAR(100),
    fecha_lanzamiento DATE,
    genero VARCHAR(100),
    precio_original DECIMAL(6,2),
    precio_descuento DECIMAL(6,2)
);

CREATE TABLE COMPRA (
    compra_id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT,
    videojuego_id INT,
    fecha_compra DATE,
    precio_pagado DECIMAL(6,2),
    FOREIGN KEY (cliente_id) REFERENCES CLIENTE(cliente_id),
    FOREIGN KEY (videojuego_id) REFERENCES VIDEOJUEGO(videojuego_id)
);

```


## Registro de Datos

```mysql

-- Insertar CLIENTES (5 ejemplos)
INSERT INTO CLIENTE (nombre_usuario, correo, pais) VALUES 
('juan_gamer', 'juan@mail.com', 'México'),
('ana_playz', 'ana@mail.com', 'Chile'),
('carlos_dev', 'carlos@mail.com', 'Perú'),
('luna_stream', 'luna@mail.com', 'Argentina'),
('mario8bit', 'mario@mail.com', 'México');

-- Insertar VIDEOJUEGOS (5 ejemplos)
INSERT INTO VIDEOJUEGO (nombre, desarrollador, publisher, fecha_lanzamiento, genero, precio_original, precio_descuento) VALUES 
('DOOM Eternal', 'id Software', 'Bethesda', '2020-03-20', 'FPS', 59.99, 29.99),
('Stardew Valley', 'ConcernedApe', 'Chucklefish', '2016-02-26', 'Simulación', 14.99, NULL),
('Hollow Knight', 'Team Cherry', 'Team Cherry', '2017-02-24', 'Metroidvania', 14.99, 9.99),
('Among Us', 'Innersloth', 'Innersloth', '2018-06-15', 'Party', 5.00, NULL),
('Cyberpunk 2077', 'CD Projekt', 'CD Projekt', '2020-12-10', 'RPG', 69.99, 39.99);

-- Insertar COMPRAS (10 ejemplos)
INSERT INTO COMPRA (cliente_id, videojuego_id, fecha_compra, precio_pagado) VALUES 
(1, 1, '2023-06-01', 29.99),
(1, 2, '2023-06-15', 14.99),
(2, 3, '2023-07-10', 9.99),
(3, 4, '2023-07-11', 5.00),
(4, 5, '2023-07-12', 39.99),
(2, 1, '2023-07-20', 29.99),
(5, 2, '2023-07-25', 14.99),
(3, 3, '2023-08-01', 9.99),
(5, 4, '2023-08-03', 5.00),
(4, 5, '2023-08-10', 39.99);

```