# ☕ Sistema de Reservas y Procesamiento de Pedidos de una Cafetería

Se solicita desarrollar un sistema para gestionar los **pedidos de una cafetería**. El sistema administra productos, categorías de productos, clientes y el cálculo del importe de los pedidos.

## 🥐 Productos y categorías de pedido

Cada producto posee un **nombre**, un **precio base** y una **cantidad disponible**.

Los pedidos pueden realizarse bajo las siguientes categorías:

* **Café:** mantiene el precio base.
* **Desayuno:** aplica un recargo del 50 % sobre el precio base e incluye dos medialunas.
* **Especial:** aplica un recargo del 70 % sobre el precio base e incluye un café de especialidad con arte latte.
* **Empleado:** tiene precio $0 y está destinado exclusivamente a empleados de la cafetería.

El precio base de un producto no puede ser negativo.

La cantidad disponible de un producto se reduce cuando forma parte de un pedido.

## 👤 Clientes y preferencias

Cada cliente posee un **nombre**, un indicador que determina si es **empleado de la cafetería**, una **preferencia de producto** y un **historial de pedidos**.

La preferencia puede modificarse durante la ejecución.

Las preferencias disponibles son:

* **Café**
* **Desayuno**
* **Especial**
* **Empleado**

La preferencia determina la categoría de producto que el cliente desea pedir.

Un cliente que sea empleado puede utilizar la preferencia **Empleado**. Un empleado también puede modificar su preferencia y realizar un pedido de cualquier otra categoría.

La preferencia **Empleado** debe verificar que el cliente sea empleado antes de permitir el pedido.

El cliente debe poder consultar el **costo total de sus pedidos**, calculado como la suma de los importes de todos los pedidos que forman parte de su historial.

## 📝 Pedidos

Al realizar un pedido de un producto, la categoría en la que se efectúa el pedido (Café, Desayuno, Especial o Empleado) queda determinada por la preferencia configurada por el cliente.

El pedido registra:

* cliente;
* producto;
* cantidad;
* importe total.

Al realizar el pedido, se descuenta del stock del producto la cantidad correspondiente.

El historial de pedidos se conserva asociado al cliente.

Si se solicita el historial de un cliente que no posee pedidos, se debe lanzar una `ClienteSinPedidosException`.

El sistema debe permitir consultar la **cantidad total de productos pedidos**.

## 💰 Cálculo del importe

El precio unitario de un producto se obtiene aplicando la particularidad correspondiente a su categoría sobre el precio base.

Luego, el importe total del pedido se calcula considerando la cantidad de productos y la configuración financiera de la cafetería.

La cafetería posee una configuración global con:

* porcentaje de cargo de servicio;
* porcentaje de impuestos.

El cálculo se realiza en el siguiente orden:

1. **Precio unitario** según la categoría.
2. **Subtotal:** precio unitario × cantidad.
3. **Cargo de servicio:** se aplica sobre el subtotal.
4. **Impuestos:** se aplican sobre el monto obtenido luego del cargo de servicio.
5. **Total final:** importe que corresponde al pedido.

La configuración financiera puede modificarse durante la ejecución.

## ⚠️ Situaciones excepcionales

El sistema debe utilizar excepciones no chequeadas para las siguientes situaciones inválidas:

* **`CantidadInvalidaException`:** al intentar crear un pedido con una cantidad negativa o cero.
* **`PrecioNegativoException`:** al intentar instanciar un producto con un precio base menor que cero.
* **`ClienteSinPedidosException`:** al solicitar el historial de pedidos de un cliente que no posee ninguno.

## 🏗️ Restricciones de diseño

* Debe ser posible incorporar nuevas categorías de productos sin modificar las categorías existentes.
* Debe ser posible incorporar nuevas preferencias de producto sin modificar las preferencias existentes.
* Debe existir una separación clara entre clientes, preferencias, productos, pedidos y configuración financiera.
