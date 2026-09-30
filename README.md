# Parcial 1 de Programación con Objetos II - Viernes

---

> [!IMPORTANT]
> 👀 Leer todo antes de comenzar a resolver


## ⚙️ Datos necesarios y obligatorios a completar
> Borrar los datos de ejemplo y poner los datos reales

* **APELLIDO, NOMBRE**: BERDICHEVSKY, CECILIA
* **COMISIÓN**: 8
* **DNI**: 15975325

> * Cecilia Berdichevsky: fue una de las primeras programadoras de Clementina, la primera computadora de gran porte para fines científicos en Argentina instalada en 1961.

---

## 📝Consideraciones Iniciales y Criterio de evaluación

>Se evaluará cada solución prestando especial atención a:   

- **Pautas obligatorias** (descritas abajo) correctamente cumplidas.
- **Entendimiento y correcta aplicación de los conceptos vistos en la cursada**: Solo los patrones de diseño vistos (Strategy | Template Method | Singleton), reificación, manejo de excepciones no chequeadas, test unitarios: **GWT** y **AAA**.
- **Prolijidad y legibilidad** del código presentado.
- Se realizará un control exhaustivo, incluyendo distintas herramientas de análisis estático de código para identificar posibles copias entre las soluciones entregadas, incluyendo el uso de IA.
- La solución debe aplicar patrones de diseño apropiados para la problemática planteada. **El uso inadecuado de patrones descalifica el examen automáticamente**.
- El código entregado debe tener los tests suficientes que garanticen el correcto funcionamiento de la solución propuesta por el alumno (*esperado 75%+*).
- No se aceptan entregas fuera de plazo ni que no estén correctamente subidas al repositorio de Gitea de la materia.
- Las entregas que tengan un solo commit o no reflejen el progreso del proceso de solución serán desaprobadas. **Se recomienda fuertemente realizar commits/push periódicamente y asegurarse de que impactaron correctamente en el repositorio remoto**.

## 📌 Pautas obligatorias para la entrega

> Utilizaremos un sistema de 3 'checkpoints', a saber:

- :warning: El código entregado debe compilar obligatoriamente. **Un parcial entregado cuyo código no compila queda desaprobado automáticamente**.

- **Checkpoint 1**: Push inicial. Clonar el repositorio remoto, modificar este archivo en la parte superior registrando **APELLIDO, NOMBRE**, **COMISIÓN** y **DNI** con sus datos, y hacer un primer push.
- **Checkpoint 2**: Push antes de realizar el primer test.
- **Checkpoint 3**: Push al final de la entrega, al terminar sus test.

> [!NOTE]
> *Este es el mínimo requerido, pero puede (y es recomendable) hacer más pushes para estar cubiert@ ante cualquier imprevisto. El último push es el código que se corrige, pero se revisa todo el flujo de trabajo.*

> [!Warning]
>**ESTAS PAUTAS SON OBLIGATORIAS, DE NO CUMPLIRLAS, AUNQUE LA SOLUCIÓN ESTÉ PERFECTA, NO APROBARÁ EL EXAMEN** ‼️

---

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
