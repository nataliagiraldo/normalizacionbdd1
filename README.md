![image](https://github.com/nataliagiraldo/normalizacionbdd1/assets/131258170/1d5a8fc8-5969-49f9-a04a-c2876007dda5)

Para normalizar una base de datos hasta la Cuarta Forma Normal (4FN), es importante comprender los conceptos y reglas de cada forma normal y aplicarlos a cada tabla de la base de datos. A continuación, voy a expandir la información proporcionada sobre cada entidad y explicar cómo se puede aplicar la normalización:

1. Tabla "País":
- Está en 1FN, 2FN y 3FN, lo que significa que no tiene grupos repetitivos de datos, todos los valores son atómicos, no hay dependencias parciales en su clave primaria y no hay dependencias transitivas.
- Para alcanzar la 4FN, debemos revisar si existen dependencias multivaluadas o dependencias de join en esta tabla y realizar ajustes en caso de ser necesario. Si no hay ninguna de estas dependencias, la tabla ya está en 4FN.

2. Tabla "Región":
- Igual que la tabla "País", está en 1FN, 2FN y 3FN.
- Para la 4FN, se deben analizar las dependencias multivaluadas o de join que pudieran existir.

3. Tabla "Ciudad":
- Sigue el mismo patrón que las anteriores y está en 1FN, 2FN y 3FN.
- Para la 4FN, se necesita examinar las dependencias multivaluadas o de join.

4. Tabla "Dirección":
- Al igual que las tablas anteriores, está en 1FN, 2FN y 3FN.
- Es crucial verificar si hay dependencias multivaluadas o de join para avanzar hacia la 4FN.

5. Tabla "Oficina":
- Está en 1FN, 2FN y 3FN.
- Se debe realizar una revisión detallada para detectar dependencias que pudieran afectar la 4FN.

6. Tabla "Empleado":
- Al igual que las anteriores, está en 1FN, 2FN y 3FN.
- Se deben examinar posibles dependencias multivaluadas o de join.

7. Tabla "Puesto":
- Está en 1FN, 2FN y 3FN.
- Revisar si existen dependencias multivaluadas o de join para avanzar hacia la 4FN.

8. Tabla "Cliente":
- También está en 1FN, 2FN y 3FN.
- Es necesario examinar las dependencias multivaluadas o de join.

9. Tabla "Proveedor":
- Está en 1FN, 2FN y 3FN.
- Revisar si hay dependencias multivaluadas o de join.

10. Tabla "Tipo Teléfono":
- Está en 1FN, 2FN y 3FN.
- Se debe verificar la presencia de dependencias multivaluadas o de join.

11. Tabla "Teléfono":
- Al igual que las anteriores, está en 1FN, 2FN y 3FN.
- Se debe examinar si existen dependencias multivaluadas o de join.

12. Tabla "Tipo Pago":
- Está en 1FN, 2FN y 3FN.
- Es importante verificar si hay dependencias multivaluadas o de join.

13. Tabla "Pago":
- Está en 1FN, 2FN y 3FN.
- Revisar si existen dependencias multivaluadas o de join.

14. Tabla "Contacto":
- Está en 1FN, 2FN y 3FN.
- Se debe examinar la presencia de dependencias multivaluadas o de join.

15. Tabla "Estado Pedido":
- Está en 1FN, 2FN y 3FN.
- Revisar si hay dependencias multivaluadas o de join.

16. Tabla "Gama Producto":
- Está en 1FN, 2FN y 3FN.
- Es importante verificar si existen dependencias multivaluadas o de join.

17. Tabla "Dimensiones":
- Está en 1FN, 2FN y 3FN.
- Se debe examinar la presencia de dependencias multivaluadas o de join.

18. Tabla "Producto":
- Está en 1FN, 2FN y 3FN.
- Revisar si existen dependencias multivaluadas o de join.

19. Tabla "Inventario":
- Está en 1FN, 2FN y 3FN.
- Es importante verificar si hay dependencias multivaluadas o de join.

20. Tabla "Pedido":
- Está en 1FN, 2FN y 3FN.
- Revisar si existen dependencias multivaluadas o de join.

21. Tabla "Detalle Pedido":
- Está en 1FN, 2FN y 3FN.
- Se debe examinar la presencia de dependencias multivaluadas o de join.

22. Tabla "Comentarios":
- Está en 1FN, 2FN y 3FN.
- Revisar si hay dependencias multivaluadas o de join.

Una vez se hayan identificado las dependencias multivaluadas o de join en cada tabla, se pueden aplicar las técnicas de normalización adecuadas para llevarlas a la Cuarta Forma Normal. Esto puede implicar la creación de nuevas tablas y la redefinición de las relaciones entre ellas para eliminar las dependencias problemáticas.

Consultas sobre una tabla
1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.

mysql> SELECT oficina.id, ciudad.nombre 
    -> FROM oficina
    -> INNER JOIN direccion ON oficina.id_direccion = direccion.id
    -> INNER JOIN ciudad ON direccion.id_ciudad = ciudad.id;
+----+--------+
| id | nombre |
+----+--------+
|  1 | Madrid |
|  2 | París  |
|  3 | Roma   |
+----+--------+

2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.

mysql>  SELECT oficina.id, ciudad.nombre, oficina.telefono
    -> FROM oficina
    ->     INNER JOIN direccion ON oficina.id_direccion = direccion.id
    ->     INNER JOIN ciudad ON direccion.id_ciudad = ciudad.id
    -> INNER JOIN region ON ciudad.id_region = region.id
    -> INNER JOIN pais ON region.id_pais = pais.id
    -> WHERE pais.nombre = 'España';
+----+--------+----------+
| id | nombre | telefono |
+----+--------+----------+
|  1 | Madrid |     NULL |
+----+--------+----------+

3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo
jefe tiene un código de jefe igual a 7.

mysql> SELECT e.nombre, e.apellido1, e.apellido2, e.email 
    -> FROM empleado AS e
    -> WHERE jefe = 7;
+--------+-----------+------------+-----------------------------+
| nombre | apellido1 | apellido2  | email                       |
+--------+-----------+------------+-----------------------------+
| María  | López     | Martínez   | maria.lopez@example.com     |
| Carlos | González  | Fernández  | carlos.gonzalez@example.com |
+--------+-----------+------------+-----------------------------+

4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la
empresa.

mysql> SELECT puesto.nombre AS puesto, empleado.nombre, empleado.apellido1, empleado.apellido2, empleado.email 
    -> FROM empleado
    -> JOIN puesto ON empleado.id = puesto.id
    -> WHERE empleado.jefe IS NULL;
+---------+--------+-----------+-----------+------------------------+
| puesto  | nombre | apellido1 | apellido2 | email                  |
+---------+--------+-----------+-----------+------------------------+
| Gerente | Juan   | Pérez     | García    | juan.perez@example.com |
+---------+--------+-----------+-----------+------------------------+

5. Devuelve un listado con el nombre, apellidos y puesto de aquellos
empleados que no sean representantes de ventas.

mysql> SELECT puesto.nombre AS puesto, empleado.nombre, empleado.apellido1, empleado.apellido2
    -> FROM empleado
    -> JOIN puesto ON empleado.id = puesto.id
    -> WHERE puesto.nombre NOT IN ('representante de ventas');
+---------------+--------+-----------+------------+
| puesto        | nombre | apellido1 | apellido2  |
+---------------+--------+-----------+------------+
| Gerente       | Juan   | Pérez     | García     |
| Asistente     | María  | López     | Martínez   |
| Recepcionista | Carlos | González  | Fernández  |
+---------------+--------+-----------+------------+

6. Devuelve un listado con el nombre de los todos los clientes españoles.
mysql> SELECT cliente.nombre
    -> FROM cliente 
    -> INNER JOIN direccion ON cliente.id_direccion = direccion.id
    -> INNER JOIN ciudad ON direccion.id_ciudad = ciudad.id
    -> INNER JOIN region ON ciudad.id_region = region.id
    -> INNER JOIN pais ON region.id_pais = pais.id
    -> WHERE pais.nombre = 'España';
+-----------+
| nombre    |
+-----------+
| Cliente 1 |
+-----------+

7. Devuelve un listado con los distintos estados por los que puede pasar un
pedido.

mysql> SELECT descripcion
    -> FROM estado_pedido;
+-------------+
| descripcion |
+-------------+
| En proceso  |
| Entregado   |
| Cancelado   |
+-------------+


8. Devuelve un listado con el código de cliente de aquellos clientes que
realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar
aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:
• Utilizando la función YEAR de MySQL.
• Utilizando la función DATE_FORMAT de MySQL.
• Sin utilizar ninguna de las funciones anteriores.

mysql> SELECT DISTINCT cliente.id
    -> FROM cliente
    -> INNER JOIN pago ON cliente.id = pago.id_cliente
    -> WHERE YEAR(pago.fecha) = 2008;
Empty set (0.01 sec)

mysql> 
mysql> SELECT DISTINCT cliente.id
    -> FROM cliente
    -> INNER JOIN pago ON cliente.id = pago.id_cliente
    -> WHERE DATE_FORMAT(pago.fecha, '%Y') = '2008';
Empty set (0.00 sec)

mysql> SELECT DISTINCT cliente.id
    -> FROM cliente
    -> INNER JOIN pago ON cliente.id = pago.id_cliente
    -> WHERE pago.fecha >= '2008-01-01' AND pago.fecha <= '2008-12-31';
Empty set (0.00 sec)

9. Devuelve un listado con el código de pedido, código de cliente, fecha
esperada y fecha de entrega de los pedidos que no han sido entregados a
tiempo.
mysql> SELECT id AS 'Código de Pedido', id_cliente AS 'Código de Cliente', fecha_esperada AS 'Fecha Esperada', fecha_entrega AS 'Fecha de Entrega'
    -> FROM pedido
    -> WHERE fecha_entrega > fecha_esperada;
Empty set (0.06 sec)

10. Devuelve un listado con el código de pedido, código de cliente, fecha
esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al
menos dos días antes de la fecha esperada.
• Utilizando la función ADDDATE de MySQL.
• Utilizando la función DATEDIFF de MySQL.
• ¿Sería posible resolver esta consulta utilizando el operador de suma + o
resta -?

SELECT id AS 'Código de Pedido', id_cliente AS 'Código de Cliente', fecha_esperada AS 'Fecha Esperada', fecha_entrega AS 'Fecha de Entrega'
FROM pedido
WHERE fecha_entrega < ADDDATE(fecha_esperada, -2);

SELECT id AS 'Código de Pedido', id_cliente AS 'Código de Cliente', fecha_esperada AS 'Fecha Esperada', fecha_entrega AS 'Fecha de Entrega'
FROM pedido
WHERE DATEDIFF(fecha_esperada, fecha_entrega) >= 2;

SELECT id AS 'Código de Pedido', id_cliente AS 'Código de Cliente', fecha_esperada AS 'Fecha Esperada', fecha_entrega AS 'Fecha de Entrega'
FROM pedido
WHERE fecha_esperada - fecha_entrega >= INTERVAL 2 DAY;


11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.

SELECT pedido.id AS 'Código de Pedido', pedido.id_cliente AS 'Código de Cliente', pedido.fecha_pedido AS 'Fecha de Pedido', pedido.fecha_entrega AS 'Fecha de Entrega'
FROM pedido
JOIN estado_pedido ON pedido.id_estado_pedido = estado_pedido.id
WHERE estado_pedido.descripcion = 'rechazado' AND YEAR(pedido.fecha_pedido) = 2009;

12. Devuelve un listado de todos los pedidos que han sido entregados en el
mes de enero de cualquier año.

SELECT id AS 'Código de Pedido', id_cliente AS 'Código de Cliente', fecha_esperada AS 'Fecha Esperada', fecha_entrega AS 'Fecha de Entrega'
FROM pedido
WHERE MONTH(fecha_entrega) = 1;


13. Devuelve un listado con todos los pagos que se realizaron en el
año 2008 mediante Paypal. Ordene el resultado de mayor a menor.

SELECT *
FROM pago
WHERE YEAR(fecha) = 2008 AND id_tipo_pago = (
    SELECT id
    FROM tipo_pago
    WHERE descripcion = 'Paypal'
)
ORDER BY total DESC;

14. Devuelve un listado con todas las formas de pago que aparecen en la
tabla pago. Tenga en cuenta que no deben aparecer formas de pago
repetidas.

mysql> SELECT DISTINCT descripcion
    -> FROM tipo_pago
    -> INNER JOIN pago ON tipo_pago.id = pago.id_tipo_pago
    -> ;
+------------------------+
| descripcion            |
+------------------------+
| Tarjeta de crédito     |
| Transferencia bancaria |
+------------------------+


15. Devuelve un listado con todos los productos que pertenecen a la
gama Ornamentales y que tienen más de 100 unidades en stock. El listado
deberá estar ordenado por su precio de venta, mostrando en primer lugar
los de mayor precio.

SELECT producto.id, producto.nombre, producto.precio_venta, inventario.stock
FROM producto
INNER JOIN inventario ON producto.id = inventario.id_producto
INNER JOIN gama_producto ON producto.id_gama_producto = gama_producto.id
WHERE gama_producto.descripcion_txt = 'Ornamentales' AND inventario.stock > 100
ORDER BY producto.precio_venta DESC;


16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y
cuyo representante de ventas tenga el código de empleado 11 o 30.


mysql> SELECT cliente.id, cliente.nombre
    -> FROM cliente
    -> INNER JOIN direccion ON cliente.id_direccion = direccion.id
    -> INNER JOIN ciudad ON direccion.id_ciudad = ciudad.id
    -> INNER JOIN empleado ON cliente.id_empleado = empleado.id
    -> WHERE ciudad.nombre = 'Madrid' AND (empleado.id = 11 OR empleado.id = 30);
+----+-----------+
| id | nombre    |
+----+-----------+
|  1 | Cliente 1 |
+----+-----------+

Consultas multitabla (Composición interna)
Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2. Las consultas con
sintaxis de SQL2 se deben resolver con INNER JOIN y NATURAL JOIN.
1. Obtén un listado con el nombre de cada cliente y el nombre y apellido de su
representante de ventas.

mysql> SELECT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante', e.apellido1 AS 'Apellido Representante'
    -> FROM cliente c
    -> JOIN empleado r ON c.id_empleado = r.id
    -> JOIN empleado e ON r.jefe = e.id;
+----------------+----------------------+------------------------+
| Nombre Cliente | Nombre Representante | Apellido Representante |
+----------------+----------------------+------------------------+
| Cliente 1      | Juan                 | Pérez                  |
| Cliente 2      | Juan                 | Pérez                  |
+----------------+----------------------+------------------------+
2. Muestra el nombre de los clientes que hayan realizado pagos junto con el
nombre de sus representantes de ventas.

mysql> SELECT DISTINCT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante'
    -> FROM cliente c
    -> JOIN pago p ON c.id = p.id_cliente
    -> JOIN empleado r ON c.id_empleado = r.id
    -> JOIN empleado e ON r.jefe = e.id;
+----------------+----------------------+
| Nombre Cliente | Nombre Representante |
+----------------+----------------------+
| Cliente 1      | Juan                 |
| Cliente 2      | Juan                 |
+----------------+----------------------+
3. Muestra el nombre de los clientes que no hayan realizado pagos junto con
el nombre de sus representantes de ventas.

SELECT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante'
FROM cliente c
LEFT JOIN pago p ON c.id = p.id_cliente
JOIN empleado r ON c.id_empleado = r.id
JOIN empleado e ON r.jefe = e.id
WHERE p.id IS NULL;

4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus
representantes junto con la ciudad de la oficina a la que pertenece el
representante.

mysql> SELECT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante', ciu.nombre AS 'Ciudad Representante'
    -> FROM cliente c
    -> JOIN pago p ON c.id = p.id_cliente
    -> JOIN empleado r ON c.id_empleado = r.id
    -> JOIN empleado e ON r.jefe = e.id
    -> JOIN oficina o ON e.id_oficina = o.id
    -> JOIN direccion d ON o.id_direccion = d.id
    -> JOIN ciudad ciu ON d.id_ciudad = ciu.id;
+----------------+----------------------+----------------------+
| Nombre Cliente | Nombre Representante | Ciudad Representante |
+----------------+----------------------+----------------------+
| Cliente 1      | Juan                 | Madrid               |
| Cliente 2      | Juan                 | Madrid               |
+----------------+----------------------+----------------------+

5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre
de sus representantes junto con la ciudad de la oficina a la que pertenece el
representante.

SELECT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante', ciu.nombre AS 'Ciudad Representante'
FROM cliente c
LEFT JOIN pago p ON c.id = p.id_cliente
JOIN empleado r ON c.id_empleado = r.id
JOIN empleado e ON r.jefe = e.id
JOIN oficina o ON e.id_oficina = o.id
JOIN direccion d ON o.id_direccion = d.id
JOIN ciudad ciu ON d.id_ciudad = ciu.id
WHERE p.id IS NULL;

6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada.

SELECT d.calle, d.carrera, d.numero, d.postal
FROM direccion d
JOIN ciudad c ON d.id_ciudad = c.id
JOIN cliente cl ON d.id = cl.id_direccion
WHERE c.nombre = 'Fuenlabrada';

7. Devuelve el nombre de los clientes y el nombre de sus representantes junto
con la ciudad de la oficina a la que pertenece el representante.

mysql> SELECT c.nombre AS 'Nombre Cliente', e.nombre AS 'Nombre Representante', ciu.nombre AS 'Ciudad Representante'
    -> FROM cliente c
    -> JOIN empleado r ON c.id_empleado = r.id
    -> JOIN empleado e ON r.jefe = e.id
    -> JOIN oficina o ON e.id_oficina = o.id
    -> JOIN direccion d ON o.id_direccion = d.id
    -> JOIN ciudad ciu ON d.id_ciudad = ciu.id;
+----------------+----------------------+----------------------+
| Nombre Cliente | Nombre Representante | Ciudad Representante |
+----------------+----------------------+----------------------+
| Cliente 1      | Juan                 | Madrid               |
| Cliente 2      | Juan                 | Madrid               |
+----------------+----------------------+----------------------+

8. Devuelve un listado con el nombre de los empleados junto con el nombre
de sus jefes.

mysql> SELECT e1.nombre AS 'Nombre Empleado', e2.nombre AS 'Nombre Jefe'
    -> FROM empleado e1
    -> LEFT JOIN empleado e2 ON e1.jefe = e2.id;
+-----------------+-------------+
| Nombre Empleado | Nombre Jefe |
+-----------------+-------------+
| Juan            | NULL        |
| María           | Juan        |
| Carlos          | Juan        |
+-----------------+-------------+

9. Devuelve un listado que muestre el nombre de cada empleados, el nombre
de su jefe y el nombre del jefe de sus jefe.

mysql> SELECT e1.nombre AS 'Nombre Empleado', e2.nombre AS 'Nombre Jefe', e3.nombre AS 'Nombre Jefe del Jefe'
    -> FROM empleado e1
    -> LEFT JOIN empleado e2 ON e1.jefe = e2.id
    -> LEFT JOIN empleado e3 ON e2.jefe = e3.id;
+-----------------+-------------+----------------------+
| Nombre Empleado | Nombre Jefe | Nombre Jefe del Jefe |
+-----------------+-------------+----------------------+
| Juan            | NULL        | NULL                 |
| María           | Juan        | NULL                 |
| Carlos          | Juan        | NULL                 |
+-----------------+-------------+----------------------+
10. Devuelve el nombre de los clientes a los que no se les ha entregado a
tiempo un pedido.


mysql> SELECT DISTINCT c.nombre AS 'Nombre Cliente'
    -> FROM cliente c
    -> JOIN pedido p ON c.id = p.id_cliente
    -> JOIN estado_pedido ep ON p.id_estado_pedido = ep.id
    -> WHERE ep.descripcion != 'Entregado' OR (ep.descripcion = 'Entregado' AND p.fecha_entrega > p.fecha_esperada);
+----------------+
| Nombre Cliente |
+----------------+
| Cliente 1      |
| Cliente 2      |
+----------------+


11. Devuelve un listado de las diferentes gamas de producto que ha comprado
cada cliente.

mysql> SELECT c.nombre AS 'Nombre Cliente', GROUP_CONCAT(DISTINCT gp.descripcion_txt SEPARATOR ', ') AS 'Gamas de Producto Compradas'
    -> FROM cliente c
    -> JOIN pedido p ON c.id = p.id_cliente
    -> JOIN detalle_pedido dp ON p.id = dp.id_pedido
    -> JOIN producto prod ON dp.id_producto = prod.id
    -> JOIN gama_producto gp ON prod.id_gama_producto = gp.id
    -> GROUP BY c.id;
+----------------+-----------------------------+
| Nombre Cliente | Gamas de Producto Compradas |
+----------------+-----------------------------+
| Cliente 1      | Electrodomésticos           |
| Cliente 2      | Muebles                     |
| Cliente 3      | Electrónica                 |
+----------------+-----------------------------+
Consultas multitabla (Composición externa)
Resuelva todas las consultas utilizando las cláusulas LEFT JOIN, RIGHT JOIN, NATURAL
LEFT JOIN y NATURAL RIGHT JOIN.
1. Devuelve un listado que muestre solamente los clientes que no han
realizado ningún pago.

SELECT c.nombre AS 'Nombre Cliente'
FROM cliente c
LEFT JOIN pago p ON c.id = p.id_cliente
WHERE p.id IS NULL;

2. Devuelve un listado que muestre solamente los clientes que no han
realizado ningún pedido.

SELECT c.nombre AS 'Nombre Cliente'
FROM cliente c
LEFT JOIN pedido p ON c.id = p.id_cliente
WHERE p.id IS NULL;

3. Devuelve un listado que muestre los clientes que no han realizado ningún
pago y los que no han realizado ningún pedido.


SELECT c.nombre AS 'Nombre Cliente', 'Sin Pagos' AS 'Estado'
FROM cliente c
LEFT JOIN pago p ON c.id = p.id_cliente
WHERE p.id IS NULL

UNION

SELECT c.nombre AS 'Nombre Cliente', 'Sin Pedidos' AS 'Estado'
FROM cliente c
LEFT JOIN pedido pd ON c.id = pd.id_cliente
WHERE pd.id IS NULL;

4. Devuelve un listado que muestre solamente los empleados que no tienen
una oficina asociada.

SELECT nombre AS 'Nombre Empleado'
FROM empleado
WHERE id_oficina IS NULL;

5. Devuelve un listado que muestre solamente los empleados que no tienen un
cliente asociado.

SELECT nombre AS 'Nombre Empleado'
FROM empleado
WHERE id NOT IN (SELECT id_empleado FROM cliente);

6. Devuelve un listado que muestre solamente los empleados que no tienen un
cliente asociado junto con los datos de la oficina donde trabajan.

SELECT e.nombre AS 'Nombre Empleado', o.*
FROM empleado e
JOIN oficina o ON e.id_oficina = o.id
WHERE e.id NOT IN (SELECT id_empleado FROM cliente);

7. Devuelve un listado que muestre los empleados que no tienen una oficina
asociada y los que no tienen un cliente asociado.


SELECT nombre AS 'Nombre Empleado', 'Sin Oficina' AS 'Estado'
FROM empleado
WHERE id_oficina IS NULL

UNION


SELECT nombre AS 'Nombre Empleado', 'Sin Cliente' AS 'Estado'
FROM empleado
WHERE id NOT IN (SELECT id_empleado FROM cliente);

8. Devuelve un listado de los productos que nunca han aparecido en un
pedido.

SELECT *
FROM producto
WHERE id NOT IN (SELECT id_producto FROM detalle_pedido);

9. Devuelve un listado de los productos que nunca han aparecido en un
pedido. El resultado debe mostrar el nombre, la descripción y la imagen del
producto.

SELECT nombre, descripcion, imagen
FROM producto
WHERE id NOT IN (SELECT id_producto FROM detalle_pedido);


10. Devuelve las oficinas donde no trabajan ninguno de los empleados que
hayan sido los representantes de ventas de algún cliente que haya realizado
la compra de algún producto de la gama Frutales.

mysql> SELECT DISTINCT o.*
    -> FROM oficina o
    -> LEFT JOIN empleado e ON o.id = e.id_oficina
    -> WHERE e.id IS NULL OR e.id NOT IN (
    ->     SELECT r.id
    ->     FROM empleado r
    ->     JOIN cliente c ON r.id = c.id_empleado
    ->     JOIN pedido p ON c.id = p.id_cliente
    ->     JOIN detalle_pedido dp ON p.id = dp.id_pedido
    ->     JOIN producto prod ON dp.id_producto = prod.id
    ->     JOIN gama_producto gp ON prod.id_gama_producto = gp.id
    ->     WHERE gp.descripcion_txt = 'Frutales'
    -> );
+----+--------------+----------+
| id | id_direccion | telefono |
+----+--------------+----------+
|  1 |            1 |     NULL |
|  2 |            2 |     NULL |
|  3 |            3 |     NULL |
+----+--------------+----------+
11. Devuelve un listado con los clientes que han realizado algún pedido pero no
han realizado ningún pago.

SELECT c.nombre AS 'Nombre Cliente'
FROM cliente c
WHERE c.id IN (SELECT id_cliente FROM pedido)
  AND c.id NOT IN (SELECT id_cliente FROM pago);

12. Devuelve un listado con los datos de los empleados que no tienen clientes
asociados y el nombre de su jefe asociado.

SELECT e.nombre AS 'Nombre Empleado', e.apellido1 AS 'Apellido Empleado', e.apellido2 AS 'Segundo Apellido Empleado', j.nombre AS 'Nombre Jefe', j.apellido1 AS 'Apellido Jefe', j.apellido2 AS 'Segundo Apellido Jefe'
FROM empleado e
LEFT JOIN empleado j ON e.jefe = j.id
WHERE e.id NOT IN (SELECT id_empleado FROM cliente);

Consultas resumen
1. ¿Cuántos empleados hay en la compañía?

mysql> SELECT COUNT(*) AS 'Total Empleados'
    -> FROM empleado;
+-----------------+
| Total Empleados |
+-----------------+
|               3 |
+-----------------+
2. ¿Cuántos clientes tiene cada país?

mysql> SELECT p.nombre AS 'País', COUNT(c.id) AS 'Total Clientes'
    -> FROM pais p
    -> LEFT JOIN region r ON p.id = r.id_pais
    -> LEFT JOIN ciudad ci ON r.id = ci.id_region
    -> LEFT JOIN direccion d ON ci.id = d.id_ciudad
    -> LEFT JOIN cliente c ON d.id = c.id_direccion
    -> GROUP BY p.nombre;
+---------+----------------+
| País    | Total Clientes |
+---------+----------------+
| España  |              1 |
| Francia |              1 |
| Italia  |              1 |
+---------+----------------+

3. ¿Cuál fue el pago medio en 2009?

SELECT AVG(total) AS 'Pago Medio 2009'
FROM pago
WHERE YEAR(fecha) = 2009;

4. ¿Cuántos pedidos hay en cada estado? Ordena el resultado de forma
descendente por el número de pedidos.

mysql> SELECT estado_pedido.descripcion AS 'Estado', COUNT(pedido.id) AS 'Número de Pedidos'
    -> FROM estado_pedido
    -> LEFT JOIN pedido ON estado_pedido.id = pedido.id_estado_pedido
    -> GROUP BY estado_pedido.descripcion
    -> ORDER BY COUNT(pedido.id) DESC;
+------------+--------------------+
| Estado     | Número de Pedidos  |
+------------+--------------------+
| En proceso |                  2 |
| Entregado  |                  1 |
| Cancelado  |                  0 |
+------------+--------------------+
5. Calcula el precio de venta del producto más caro y más barato en una
misma consulta.

mysql> SELECT 
    ->     MAX(precio_venta) AS 'Precio Más Caro',
    ->     MIN(precio_venta) AS 'Precio Más Barato'
    -> FROM producto;
+------------------+--------------------+
| Precio Más Caro  | Precio Más Barato  |
+------------------+--------------------+
|              700 |                500 |
+------------------+--------------------+

6. Calcula el número de clientes que tiene la empresa.

mysql> SELECT COUNT(*) AS 'Número de Clientes'
    -> FROM cliente;
+---------------------+
| Número de Clientes  |
+---------------------+
|                   3 |
+---------------------+
7. ¿Cuántos clientes existen con domicilio en la ciudad de Madrid?


mysql> SELECT COUNT(*) AS 'Clientes en Madrid'
    -> FROM cliente c
    -> JOIN direccion d ON c.id_direccion = d.id
    -> JOIN ciudad ci ON d.id_ciudad = ci.id
    -> WHERE ci.nombre = 'Madrid';
+--------------------+
| Clientes en Madrid |
+--------------------+
|                  1 |
+--------------------+

8. ¿Calcula cuántos clientes tiene cada una de las ciudades que empiezan
por M?


mysql> SELECT ci.nombre AS 'Ciudad', COUNT(c.id) AS 'Total Clientes'
    -> FROM ciudad ci
    -> JOIN direccion d ON ci.id = d.id_ciudad
    -> JOIN cliente c ON d.id = c.id_direccion
    -> WHERE ci.nombre LIKE 'M%'
    -> GROUP BY ci.nombre;
+--------+----------------+
| Ciudad | Total Clientes |
+--------+----------------+
| Madrid |              1 |
+--------+----------------+

9. Devuelve el nombre de los representantes de ventas y el número de clientes
al que atiende cada uno.

mysql> SELECT e.nombre AS 'Representante de Ventas', COUNT(c.id) AS 'Número de Clientes'
    -> FROM empleado e
    -> LEFT JOIN cliente c ON e.id = c.id_empleado
    -> WHERE e.jefe IS NULL
    -> GROUP BY e.nombre;
+-------------------------+---------------------+
| Representante de Ventas | Número de Clientes  |
+-------------------------+---------------------+
| Juan                    |                   1 |
+-------------------------+---------------------+

10. Calcula el número de clientes que no tiene asignado representante de
ventas.

mysql> SELECT COUNT(*) AS 'Clientes sin Representante'
    -> FROM cliente
    -> WHERE id_empleado IS NULL;
+----------------------------+
| Clientes sin Representante |
+----------------------------+
|                          0 |
+----------------------------+

11. Calcula la fecha del primer y último pago realizado por cada uno de los
clientes. El listado deberá mostrar el nombre y los apellidos de cada cliente.

mysql> SELECT 
    ->     c.nombre AS 'Nombre Cliente',
    ->     MIN(p.fecha) AS 'Primer Pago',
    ->     MAX(p.fecha) AS 'Último Pago'
    -> FROM 
    ->     cliente c
    -> LEFT JOIN 
    ->     pago p ON c.id = p.id_cliente
    -> GROUP BY 
    ->     c.nombre;
+----------------+-------------+--------------+
| Nombre Cliente | Primer Pago | Último Pago  |
+----------------+-------------+--------------+
| Cliente 1      | 2023-01-15  | 2023-01-15   |
| Cliente 2      | 2023-02-20  | 2023-02-20   |
| Cliente 3      | 2023-03-10  | 2023-03-10   |
+----------------+-------------+--------------+
12. Calcula el número de productos diferentes que hay en cada uno de los
pedidos.

mysql> SELECT id_pedido, COUNT(DISTINCT id_producto) AS 'Número de Productos'
    -> FROM detalle_pedido
    -> GROUP BY id_pedido;
+-----------+----------------------+
| id_pedido | Número de Productos  |
+-----------+----------------------+
|         1 |                    1 |
|         2 |                    1 |
|         3 |                    1 |
+-----------+----------------------+

13. Calcula la suma de la cantidad total de todos los productos que aparecen en
cada uno de los pedidos.

mysql> SELECT id_pedido, SUM(cantidad) AS 'Cantidad Total'
    -> FROM detalle_pedido
    -> GROUP BY id_pedido;
+-----------+----------------+
| id_pedido | Cantidad Total |
+-----------+----------------+
|         1 |              2 |
|         2 |              1 |
|         3 |              3 |
+-----------+----------------+
14. Devuelve un listado de los 20 productos más vendidos y el número total de
unidades que se han vendido de cada uno. El listado deberá estar ordenado
por el número total de unidades vendidas.

mysql> SELECT 
    ->     dp.id_producto,
    ->     p.nombre AS 'Nombre Producto',
    ->     SUM(dp.cantidad) AS 'Total Unidades Vendidas'
    -> FROM 
    ->     detalle_pedido dp
    -> JOIN 
    ->     producto p ON dp.id_producto = p.id
    -> GROUP BY 
    ->     dp.id_producto, p.nombre
    -> ORDER BY 
    ->     SUM(dp.cantidad) DESC
    -> LIMIT 20;
+-------------+-----------------+-------------------------+
| id_producto | Nombre Producto | Total Unidades Vendidas |
+-------------+-----------------+-------------------------+
|           3 | Smartphone      |                       3 |
|           1 | Lavadora        |                       2 |
|           2 | Sofá            |                       1 |
+-------------+-----------------+-------------------------+

15. La facturación que ha tenido la empresa en toda la historia, indicando la
base imponible, el IVA y el total facturado. La base imponible se calcula
sumando el coste del producto por el número de unidades vendidas de la
tabla detalle_pedido. El IVA es el 21 % de la base imponible, y el total la
suma de los dos campos anteriores.

mysql> SELECT 
    ->     SUM(dp.precio_unidad * dp.cantidad) AS 'Base Imponible',
    ->     SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'IVA',
    ->     SUM(dp.precio_unidad * dp.cantidad) + SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'Total Facturado'
    -> FROM 
    ->     detalle_pedido dp;
+----------------+------+-----------------+
| Base Imponible | IVA  | Total Facturado |
+----------------+------+-----------------+
|           3200 |  672 |            3872 |
+----------------+------+-----------------+

16. La misma información que en la pregunta anterior, pero agrupada por
código de producto.

mysql> SELECT 
    ->     dp.id_producto AS 'Código de Producto',
    ->     SUM(dp.precio_unidad * dp.cantidad) AS 'Base Imponible',
    ->     SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'IVA',
    ->     SUM(dp.precio_unidad * dp.cantidad) + SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'Total Facturado'
    -> FROM 
    ->     detalle_pedido dp
    -> GROUP BY 
    ->     dp.id_producto;
+---------------------+----------------+------+-----------------+
| Código de Producto  | Base Imponible | IVA  | Total Facturado |
+---------------------+----------------+------+-----------------+
|                   1 |            500 |  105 |             605 |
|                   2 |            600 |  126 |             726 |
|                   3 |           2100 |  441 |            2541 |
+---------------------+----------------+------+-----------------+

17. La misma información que en la pregunta anterior, pero agrupada por
código de producto filtrada por los códigos que empiecen por OR

mysql> SELECT 
    ->     dp.id_producto AS 'Código de Producto',
    ->     SUM(dp.precio_unidad * dp.cantidad) AS 'Base Imponible',
    ->     SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'IVA',
    ->     SUM(dp.precio_unidad * dp.cantidad) + SUM(dp.precio_unidad * dp.cantidad * 0.21) AS 'Total Facturado'
    -> FROM 
    ->     detalle_pedido dp
    -> JOIN
    ->     producto p ON dp.id_producto = p.id
    -> JOIN
    ->     gama_producto gp ON p.id_gama_producto = gp.id
    -> WHERE
    ->     gp.descripcion_txt LIKE 'OR%'
    -> GROUP BY 
    ->     dp.id_producto;
+---------------------+----------------+------+-----------------+
| Código de Producto  | Base Imponible | IVA  | Total Facturado |
+---------------------+----------------+------+-----------------+
|                   1 |            500 |  105 |             605 |
|                   2 |            600 |  126 |             726 |
|                   3 |           2100 |  441 |            2541 |
+---------------------+----------------+------+-----------------+

18. Lista las ventas totales de los productos que hayan facturado más de 3000
euros. Se mostrará el nombre, unidades vendidas, total facturado y total
facturado con impuestos (21% IVA).

SELECT 
    p.nombre AS 'Nombre del Producto',
    SUM(dp.cantidad) AS 'Unidades Vendidas',
    SUM(dp.precio_unidad * dp.cantidad) AS 'Total Facturado',
    SUM(dp.precio_unidad * dp.cantidad) * 1.21 AS 'Total Facturado con Impuestos'
FROM 
    detalle_pedido dp
JOIN 
    producto p ON dp.id_producto = p.id
GROUP BY 
    p.nombre
HAVING 
    SUM(dp.precio_unidad * dp.cantidad) > 3000;

19. Muestre la suma total de todos los pagos que se realizaron para cada uno
de los años que aparecen en la tabla pagos.

mysql> SELECT YEAR(fecha) AS 'Año', SUM(total) AS 'Total Pagado'
    -> FROM pago
    -> GROUP BY YEAR(fecha);
+------+--------------+
| Año  | Total Pagado |
+------+--------------+
| 2023 |        451.5 |
+------+--------------+

Consultas variadas
1. Devuelve el listado de clientes indicando el nombre del cliente y cuántos
pedidos ha realizado. Tenga en cuenta que pueden existir clientes que no
han realizado ningún pedido.

mysql> SELECT 
    ->     c.nombre AS 'Nombre del Cliente',
    ->     COUNT(p.id) AS 'Cantidad de Pedidos'
    -> FROM 
    ->     cliente c
    -> LEFT JOIN 
    ->     pedido p ON c.id = p.id_cliente
    -> GROUP BY 
    ->     c.nombre;
+--------------------+---------------------+
| Nombre del Cliente | Cantidad de Pedidos |
+--------------------+---------------------+
| Cliente 1          |                   1 |
| Cliente 2          |                   1 |
| Cliente 3          |                   1 |
+--------------------+---------------------+

2. Devuelve un listado con los nombres de los clientes y el total pagado por
cada uno de ellos. Tenga en cuenta que pueden existir clientes que no han
realizado ningún pago.

mysql> SELECT 
    ->     c.nombre AS 'Nombre del Cliente',
    ->     COALESCE(SUM(p.total), 0) AS 'Total Pagado'
    -> FROM 
    ->     cliente c
    -> LEFT JOIN 
    ->     pago p ON c.id = p.id_cliente
    -> GROUP BY 
    ->     c.nombre;
+--------------------+--------------+
| Nombre del Cliente | Total Pagado |
+--------------------+--------------+
| Cliente 1          |        100.5 |
| Cliente 2          |       200.75 |
| Cliente 3          |       150.25 |
+--------------------+--------------+
3. Devuelve el nombre de los clientes que hayan hecho pedidos en 2008
ordenados alfabéticamente de menor a mayor.

SELECT DISTINCT
    c.nombre AS 'Nombre del Cliente'
FROM 
    cliente c
JOIN 
    pedido p ON c.id = p.id_cliente
WHERE 
    YEAR(p.fecha_pedido) = 2008
ORDER BY 
    c.nombre ASC;

4. Devuelve el nombre del cliente, el nombre y primer apellido de su
representante de ventas y el número de teléfono de la oficina del
representante de ventas, de aquellos clientes que no hayan realizado ningún
pago.

SELECT 
    c.nombre AS 'Nombre del Cliente',
    CONCAT(e.nombre, ' ', e.apellido1) AS 'Nombre del Representante',
    t.numero AS 'Número de Teléfono de la Oficina'
FROM 
    cliente c
JOIN 
    empleado e ON c.id_empleado = e.id
JOIN 
    oficina o ON e.id_oficina = o.id
JOIN 
    telefono t ON o.telefono = t.id
LEFT JOIN 
    pago p ON c.id = p.id_cliente
WHERE 
    p.id IS NULL;

5. Devuelve el listado de clientes donde aparezca el nombre del cliente, el
nombre y primer apellido de su representante de ventas y la ciudad donde
está su oficina.

mysql> SELECT 
    ->     c.nombre AS 'Nombre del Cliente',
    ->     CONCAT(e.nombre, ' ', e.apellido1) AS 'Nombre del Representante',
    ->     ci.nombre AS 'Ciudad de la Oficina'
    -> FROM 
    ->     cliente c
    -> JOIN 
    ->     empleado e ON c.id_empleado = e.id
    -> JOIN 
    ->     oficina o ON e.id_oficina = o.id
    -> JOIN 
    ->     direccion d ON o.id_direccion = d.id
    -> JOIN 
    ->     ciudad ci ON d.id_ciudad = ci.id;
+--------------------+--------------------------+----------------------+
| Nombre del Cliente | Nombre del Representante | Ciudad de la Oficina |
+--------------------+--------------------------+----------------------+
| Cliente 1          | María López              | París                |
| Cliente 2          | Carlos González          | Madrid               |
| Cliente 3          | Juan Pérez               | Madrid               |
+--------------------+--------------------------+----------------------+

6. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos
empleados que no sean representante de ventas de ningún cliente.

SELECT 
    e.nombre AS 'Nombre del Empleado',
    CONCAT(e.apellido1, ' ', COALESCE(e.apellido2, '')) AS 'Apellidos',
    p.nombre AS 'Puesto',
    t.numero AS 'Teléfono de la Oficina'
FROM 
    empleado e
JOIN 
    oficina o ON e.id_oficina = o.id
JOIN 
    puesto p ON e.id = p.id
JOIN 
    telefono t ON o.telefono = t.id
LEFT JOIN 
    cliente c ON e.id = c.id_empleado
WHERE 
    c.id_empleado IS NULL
    OR c.id_empleado = '';

7. Devuelve un listado indicando todas las ciudades donde hay oficinas y el
número de empleados que tiene.

mysql> SELECT 
    ->     ci.nombre AS 'Ciudad',
    ->     COUNT(e.id) AS 'Número de Empleados'
    -> FROM 
    ->     ciudad ci
    -> JOIN 
    ->     direccion d ON ci.id = d.id_ciudad
    -> JOIN 
    ->     oficina o ON d.id = o.id_direccion
    -> JOIN 
    ->     empleado e ON o.id = e.id_oficina
    -> GROUP BY 
    ->     ci.nombre;
+--------+----------------------+
| Ciudad | Número de Empleados  |
+--------+----------------------+
| Madrid |                    2 |
| París  |                    1 |
+--------+----------------------+
