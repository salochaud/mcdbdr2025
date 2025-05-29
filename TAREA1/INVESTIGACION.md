# Tarea 1 
 ## Descripción de una Base de Datos 

 Durante el tetramestre se trabajará con una base de datos para una tienda en línea de videojuegos, que almacena información sobre los videojuegos disponibles, los clientes registrados y las compras que realizan.

Las entidades principales y sus atributos (con su tipo de dato) son:

1. Clientes
- id_cliente (entero): identificador único del cliente.
- nombre (texto): nombre completo del cliente.
- correo (texto): correo electrónico del cliente.
- fecha_registro (fecha): fecha en que se registró el cliente en la tienda.

2. Videojuegos
- id_videojuego (entero): identificador único del videojuego.
- titulo (texto): nombre del videojuego.
- plataforma (texto): consola o sistema.
- precio (decimal): precio en moneda local.
- fecha_lanzamiento (fecha): fecha en que se lanzó el juego.

3. Compras
- id_compra (entero): identificador único de la compra.
- id_cliente (entero): hace referencia al cliente que realizó la compra.
- id_videojuego (entero): hace referencia al videojuego comprado.
- fecha_compra (fecha): fecha en que se realizó la compra.
- monto (decimal): total pagado por el videojuego.

Relaciones:
- Un cliente puede hacer muchas compras, cada compra pertenece a un solo cliente.
- Un videojuego puede ser comprado muchas veces por diferentes clientes.
- Cada compra conecta a un cliente con un videojuego específico.

 ## Investigacion SGBD "MySQL"
MySQL se dio a conocer a finales de la década de 1990 como un sistema de gestión de bases de datos relacional especialmente adecuado para pequeños proyectos web, aprovechando sobre todo de su carácter gratuito y su rapidez. Después, en el transcurso de los años 2000, los gigantes de la Web se pusieron a utilizar MySQL de forma masiva. Lo siguiente fue más difícil, ya que en la segunda mitad de la década de 2000 todos estos grandes actores tuvieron que hacer frente a las limitaciones de MySQL en cuanto a su escalabilidad. Fue en ese momento cuando surgieron muchas soluciones NoSQL. Pero, finalmente, MySQL ha evolucionado de forma rápida en los últimos años, mientras que los problemas de juventud de las soluciones NoSQL se han hecho cada vez más evidentes.

Hoy en día, MySQL sigue siendo una opción muy extendida para proyectos web, mucho menos para proyectos más tradicionales. ¿Cuáles son las razones? En primer lugar, MySQL es capaz de ofrecer buenos rendimientos incluso con los servidores menos potentes. Además, su estabilidad es excelente y, en una instancia configurada de forma correcta, es muy raro que MySQL se cuelgue o pierda los datos. Por último, su carácter gratuito permite contemplar despliegues con cientos o miles de instancias en caso necesario sin gastar una fortuna en licencias.

> Referencias:

> MySQL 5.7. (n.d.). Google Books. https://books.google.com.mx/books?hl=es&lr=&id=QpYLonKfIesC&oi=fnd&pg=PA236&dq=mysql&ots=N3fsceDpPI&sig=edX8R8tArUo_Cpq4ayiapi4Mzlc&redir_esc=y#v=onepage&q=mysql&f=false


