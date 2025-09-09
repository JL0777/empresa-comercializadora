# Casos de Uso

---

## CU01 – Gestionar productos
**Actor principal:** Administrador  
**Descripción:** El administrador puede agregar, editar e inhabilitar productos con sus especificaciones (nombre, talla, precio, proveedor, categoría) para mantener actualizado el catálogo.  

**Precondiciones:**
- El administrador debe haber iniciado sesión en el sistema.
- Deben existir proveedores registrados.

**Flujo principal:**
1. El administrador selecciona la opción "Gestionar productos".
2. El sistema muestra la lista de productos existentes.
3. El administrador elige entre agregar, editar o inhabilitar un producto.
4. El sistema solicita los datos requeridos (nombre, talla, precio, categoría, proveedor).
5. El administrador confirma la operación.
6. El sistema guarda los cambios y actualiza el catálogo.

**Flujos alternativos:**
- 3a. Si el producto ya existe y se intenta registrar uno con el mismo código → El sistema muestra mensaje de error.
- 5a. Si el administrador cancela la operación → El sistema no guarda cambios.

**Postcondiciones:**
- El catálogo queda actualizado con la información ingresada por el administrador.

---

## CU02 – Gestionar usuarios
**Actor principal:** Administrador  
**Descripción:** El administrador puede registrar, modificar y dar de baja usuarios del sistema (administradores, vendedores, clientes).  

**Precondiciones:**
- El administrador debe estar autenticado en el sistema.

**Flujo principal:**
1. El administrador selecciona la opción "Gestionar usuarios".
2. El sistema muestra la lista de usuarios registrados.
3. El administrador elige entre agregar, editar o eliminar un usuario.
4. El sistema solicita datos del usuario (nombre, rol, credenciales).
5. El administrador confirma la operación.
6. El sistema guarda y actualiza la información del usuario.

**Flujos alternativos:**
- 3a. Si se intenta eliminar un usuario con ventas asociadas → El sistema pide confirmación especial.
- 5a. Si el administrador cancela la operación → No se realizan cambios.

**Postcondiciones:**
- El sistema mantiene actualizado el control de accesos y roles.

---

## CU03 – Consultar inventario
**Actor principal:** Administrador  
**Descripción:** El administrador puede consultar el inventario completo con detalles de stock y proveedores.  

**Precondiciones:**
- Deben existir productos registrados en el sistema.

**Flujo principal:**
1. El administrador selecciona la opción "Consultar inventario".
2. El sistema muestra la lista de productos con stock, proveedor y estado.
3. El administrador puede filtrar por categoría, talla o proveedor.

**Postcondiciones:**
- El administrador obtiene información actualizada para control operativo.

---

## CU04 – Generar reportes generales
**Actor principal:** Administrador  
**Descripción:** El administrador puede generar reportes generales de ventas (diarios, semanales, mensuales).  

**Precondiciones:**
- Deben existir ventas registradas en el sistema.

**Flujo principal:**
1. El administrador selecciona la opción "Reportes de ventas".
2. El sistema solicita rango de fechas y tipo de reporte.
3. El administrador confirma la generación.
4. El sistema procesa la información y genera el reporte.
5. El administrador visualiza o descarga el reporte.

**Postcondiciones:**
- Se genera un reporte con la información de ventas solicitada.

---

## CU05 – Gestionar nómina de vendedores
**Actor principal:** Administrador  
**Descripción:** El administrador puede calcular y registrar la nómina de los vendedores en función de sus ventas.  

**Precondiciones:**
- Deben existir vendedores registrados.
- Deben existir ventas registradas.

**Flujo principal:**
1. El administrador selecciona la opción "Gestión de nómina".
2. El sistema muestra lista de vendedores y sus ventas.
3. El administrador ingresa parámetros de cálculo (comisiones, bonos, descuentos).
4. El sistema calcula la nómina correspondiente.
5. El administrador confirma la operación.
6. El sistema guarda los registros de nómina.

**Postcondiciones:**
- El sistema mantiene la información financiera de los vendedores actualizada.

---

## CU06 – Registrar venta
**Actor principal:** Vendedor  
**Descripción:** El vendedor puede registrar una venta con múltiples productos, cantidades, tallas y precios, seleccionando el nombre del vendedor que realizó la venta.  

**Precondiciones:**
- Deben existir productos en inventario.
- Deben estar registrados vendedores por el administrador.

**Flujo principal:**
1. El vendedor selecciona la opción "Registrar venta".
2. El sistema solicita el nombre del vendedor responsable.
3. El vendedor ingresa los productos vendidos, cantidades y tallas.
4. El sistema calcula el total de la venta.
5. El vendedor confirma la operación.
6. El sistema registra la venta y actualiza el inventario.

**Flujos alternativos:**
- 3a. Si no hay stock suficiente → El sistema muestra mensaje de error.
- 5a. Si el vendedor cancela → La venta no se guarda.

**Postcondiciones:**
- La venta queda registrada y el inventario se actualiza.

---

## CU07 – Consultar ventas realizadas
**Actor principal:** Vendedor  
**Descripción:** El vendedor puede consultar el historial de ventas realizadas, filtrando por fecha.  

**Precondiciones:**
- Deben existir ventas registradas.

**Flujo principal:**
1. El vendedor selecciona la opción "Consultar ventas".
2. El sistema solicita rango de fechas.
3. El vendedor ingresa los filtros.
4. El sistema muestra listado de ventas correspondientes.

**Postcondiciones:**
- El vendedor obtiene el historial de ventas solicitado.

---

## CU08 – Gestionar inventario operativo
**Actor principal:** Vendedor  
**Descripción:** El vendedor puede consultar productos disponibles y actualizar el stock tras una venta.  

**Precondiciones:**
- Deben existir productos en inventario.

**Flujo principal:**
1. El vendedor selecciona la opción "Inventario operativo".
2. El sistema muestra lista de productos y stock actual.
3. Tras registrar una venta, el sistema descuenta automáticamente el stock.
4. El vendedor puede consultar disponibilidad de productos en cualquier momento.

**Postcondiciones:**
- El inventario se mantiene actualizado en tiempo real.

---

## CU09 – Visualizar productos disponibles
**Actor principal:** Cliente  
**Descripción:** El cliente puede visualizar los productos con sus detalles (nombre, talla, categoría, precio, especificaciones).  

**Precondiciones:**
- Deben existir productos habilitados en el catálogo.

**Flujo principal:**
1. El cliente accede a la tienda en línea.
2. El sistema muestra los productos disponibles.
3. El cliente visualiza detalles de cada producto.

**Postcondiciones:**
- El cliente obtiene información para decidir su compra.

---

## CU10 – Buscar productos
**Actor principal:** Cliente  
**Descripción:** El cliente puede buscar productos por nombre, categoría o talla.  

**Precondiciones:**
- Deben existir productos habilitados en el catálogo.

**Flujo principal:**
1. El cliente accede a la opción de búsqueda.
2. El cliente ingresa el criterio de búsqueda.
3. El sistema filtra y muestra los resultados correspondientes.

**Postcondiciones:**
- El cliente localiza fácilmente el producto que necesita.

---
