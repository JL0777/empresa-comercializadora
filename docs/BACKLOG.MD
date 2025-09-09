# Definir estructura de base de datos  

## Objetivo  
Diseñar la base de datos que permita gestionar **usuarios, sucursales, productos, ventas e inventario**, y que además soporte el cálculo de la **nómina diaria** de los vendedores siguiendo el esquema definido:  

- Cada vendedor recibe un **básico de 50.000 pesos**.  
- En las **ventas con comisión** (precio venta > precio mínimo), la diferencia es un **código de sobreventa**. Al final del día:  
  - La mitad de la suma de códigos queda para el almacén.  
  - La otra mitad se divide equitativamente entre los vendedores.  
- En las **ventas sin comisión**, se toma el total vendido, se multiplica por el **2%**, y se divide entre todos los vendedores.  
- Los reportes deben permitir ver tanto las ventas por vendedor como los pagos diarios acumulados.  

---

## Organización de la base de datos  

La base de datos se organiza en cuatro grandes bloques:  

1. **Gestión de usuarios y roles**  
   - Controlar administradores, vendedores y clientes.  
   - Relacionar vendedores con sucursales y ventas registradas.  

2. **Gestión de productos, inventario y proveedores**  
   - Guardar productos con especificaciones, precio mínimo y proveedor.  
   - Mantener stock actualizado.  

3. **Gestión de sucursales**  
   - Permitir separar Local y Sublocal.  
   - Facilitar reportes de ventas por ubicación.  

4. **Gestión de ventas y nómina**  
   - Registrar ventas con sus detalles (productos, cantidades, precios).  
   - Diferenciar ventas con comisión y sin comisión.  
   - Generar y almacenar cálculos de nómina diaria para cada vendedor.  

---

## Tablas principales  

### 1. **Sucursales**  
- `sucursal_id` (PK)  
- `nombre`  
- `tipo` (Local / Sublocal)  
- `direccion`  
- `estado`  

---

### 2. **Usuarios**  
- `usuario_id` (PK)  
- `nombre`  
- `documento` (CC/NIT)  
- `rol` (Administrador / Vendedor / Cliente)  
- `sucursal_id` (FK → Sucursales)  
- `estado` (activo/inactivo)  
- `fecha_creacion`  

Permite gestionar roles y accesos, y asociar vendedores con una sucursal.  

---

### 3. **Productos**  
- `producto_id` (PK)  
- `codigo_producto` (único)  
- `nombre`  
- `categoria`  
- `talla`  
- `precio_minimo`  
- `precio_referencia` (para ventas sin comisión)  
- `stock`  
- `proveedor_id` (FK → Proveedores)  
- `estado` (activo/inactivo)  

El campo **precio_minimo** es clave para calcular la comisión.  

---

### 4. **Proveedores**  
- `proveedor_id` (PK)  
- `nombre`  
- `telefono`  
- `direccion`  
- `estado`  

Relación directa con los productos.  

---

### 5. **Ventas**  
- `venta_id` (PK)  
- `fecha_venta`  
- `usuario_vendedor_id` (FK → Usuarios)  
- `cliente_id` (FK → Usuarios, rol=Cliente)  
- `sucursal_id` (FK → Sucursales)  
- `total_venta`  
- `tipo` (Con comisión / Sin comisión)  
- `metodo_pago` (Efectivo / Tarjeta / Transferencia)  
- `estado` (Finalizada / Anulada)  

Es la cabecera de la venta.  

---

### 6. **Detalle_Venta**  
- `detalle_id` (PK)  
- `venta_id` (FK → Ventas)  
- `producto_id` (FK → Productos)  
- `cantidad`  
- `precio_unitario`  
- `subtotal`  
- `precio_minimo_referencia` (precio mínimo histórico al momento de la venta)  
- `sobreventa_codigo` (valor excedente sobre el precio mínimo, 0 si no aplica)  

Aquí es donde se calcula la comisión por producto vendido.  

---

### 7. **Nomina_Diaria**  
- `nomina_id` (PK)  
- `fecha`  
- `sucursal_id` (FK → Sucursales)  
- `total_sobreventa` (sumatoria de códigos del día)  
- `mitad_almacen`  
- `mitad_empleados`  
- `ventas_sin_comision` (total del día)  
- `bono_ventas_sin_comision` (2% total ventas sin comisión)  
- `numero_empleados` (activos ese día)  
- `total_empleados` (mitad_empleados + bono_sin_comision + básico*#empleados)  

Aquí se guarda el cálculo global de la nómina del día.  

---

### 8. **Nomina_Empleados**  
- `id` (PK)  
- `nomina_id` (FK → Nomina_Diaria)  
- `empleado_id` (FK → Usuarios)  
- `ventas_totales_empleado` (aportadas al total)  
- `comision_generada` (suma de códigos de sus ventas, aunque el pago sea igualitario)  
- `pago_base` (50,000)  
- `pago_comisiones` (parte proporcional de comisiones)  
- `pago_bono_sin_comision` (parte proporcional del 2%)  
- `total_pagado`  

Relaciona la nómina con cada empleado y permite ver qué generó cada uno.  

---

## Relaciones clave  

- Un **usuario vendedor** puede registrar múltiples ventas en su **sucursal**.  
- Cada **venta** tiene varios productos en detalle.  
- Cada **producto** tiene un precio mínimo que define la sobreventa.  
- La **nómina diaria** se calcula en base a todas las ventas (detalle_venta) de la fecha por sucursal.  
- La **nómina empleados** distribuye los pagos entre los vendedores activos.  
- Los reportes pueden filtrarse por **fecha, sucursal, vendedor, producto o cliente**.  

---

