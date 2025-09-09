#  Definir estructura de base de datos  

##  Objetivo  
Diseñar la base de datos que permita gestionar **usuarios, productos, ventas e inventario**, y que además soporte el cálculo de la **nómina diaria** de los vendedores siguiendo el esquema definido:  

- Cada vendedor recibe un **básico de 50.000 pesos**.  
- En las **ventas con comisión** (precio venta > precio mínimo), la diferencia es un **código de sobreventa**. Al final del día:  
  - La mitad de la suma de códigos queda para el almacén.  
  - La otra mitad se divide equitativamente entre los vendedores.  
- En las **ventas sin comisión**, se toma el total vendido, se multiplica por el **2%**, y se divide entre todos los vendedores.  
- Los reportes deben permitir ver tanto las ventas por vendedor como los pagos diarios acumulados.  

---

##  Organización de la base de datos  

La base de datos se organiza en tres grandes bloques:  

1. **Gestión de usuarios y roles**  
   - Controlar administradores, vendedores y clientes.  
   - Relacionar vendedores con las ventas registradas.  

2. **Gestión de productos e inventario**  
   - Guardar productos con sus especificaciones, precio mínimo y proveedor.  
   - Mantener stock actualizado.  

3. **Gestión de ventas y nómina**  
   - Registrar las ventas con sus detalles (productos, cantidades, precios).  
   - Diferenciar ventas con comisión y sin comisión.  
   - Generar y almacenar cálculos de nómina diaria para cada vendedor.  

---

##  Tablas principales  

### 1. **Usuarios**  
- `usuario_id` (PK)  
- `nombre`  
- `rol` (Administrador / Vendedor / Cliente)  
- `estado` (activo/inactivo)  
- `fecha_creacion`  

 Permite gestionar roles y accesos.  

---

### 2. **Productos**  
- `producto_id` (PK)  
- `nombre`  
- `categoria`  
- `talla`  
- `precio_minimo`  
- `stock`  
- `proveedor_id` (FK → Proveedores)  
- `estado` (activo/inactivo)  

 El campo **precio_minimo** es clave para calcular la comisión.  

---

### 3. **Proveedores**  
- `proveedor_id` (PK)  
- `nombre`  
- `telefono`  
- `direccion`  
- `estado`  

 Relación directa con los productos.  

---

### 4. **Ventas**  
- `venta_id` (PK)  
- `fecha_venta`  
- `usuario_vendedor_id` (FK → Usuarios)  
- `sucursal` (Local / Sublocal)  
- `total_venta`  
- `tipo` (Con comisión / Sin comisión)  

 Es la cabecera de la venta.  

---

### 5. **Detalle_Venta**  
- `detalle_id` (PK)  
- `venta_id` (FK → Ventas)  
- `producto_id` (FK → Productos)  
- `cantidad`  
- `precio_unitario`  
- `subtotal`  
- `sobreventa_codigo` (valor excedente sobre el precio mínimo, si aplica, 0 si no)  

 Aquí es donde se calcula la comisión por producto vendido.  

---

### 6. **Nomina_Diaria**  
- `nomina_id` (PK)  
- `fecha`  
- `total_sobreventa` (sumatoria de códigos del día)  
- `mitad_almacen`  
- `mitad_empleados`  
- `ventas_sin_comision` (total del día)  
- `bono_ventas_sin_comision` (2% total ventas sin comisión)  
- `total_empleados` (mitad_empleados + bono_sin_comision + básico*#empleados)  

 Aquí se guarda el cálculo global de la nómina del día.  

---

### 7. **Nomina_Empleados**  
- `id` (PK)  
- `nomina_id` (FK → Nomina_Diaria)  
- `empleado_id` (FK → Usuarios)  
- `pago_base` (50,000)  
- `pago_comisiones` (parte proporcional de comisiones)  
- `pago_bono_sin_comision` (parte proporcional del 2%)  
- `total_pagado`  

 Relaciona la nómina con cada empleado.  

---

##  Relaciones clave  

- Un **usuario vendedor** puede registrar múltiples ventas.  
- Cada **venta** tiene varios productos en detalle.  
- Cada **producto** tiene un precio mínimo que define la sobreventa.  
- La **nómina diaria** se calcula en base a todas las ventas (detalle_venta) de la fecha.  
- La **nómina empleados** distribuye los pagos entre los vendedores activos.  

---