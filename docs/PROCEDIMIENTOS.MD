# Planificación de Procedimientos, Triggers y Vistas  

## Objetivo  
Definir los procedimientos, triggers y vistas que faciliten la gestión del sistema, el cálculo automático de nómina y la generación de reportes.  

---

## 1. Procedimientos almacenados (Stored Procedures)  

### 1.1 Registrar venta  
- Inserta en `Ventas` y `Detalle_Venta`.  
- Calcula `sobreventa_codigo` automáticamente.  
- Actualiza el `stock` en `Productos`.  

### 1.2 Cerrar nómina diaria  
- Recorre ventas del día por sucursal.  
- Suma códigos de sobreventa.  
- Calcula mitad para almacén y mitad para empleados.  
- Suma el 2% de ventas sin comisión.  
- Inserta en `Nomina_Diaria`.  
- Reparte entre empleados y guarda en `Nomina_Empleados`.  

### 1.3 Consultar ventas por vendedor  
- Devuelve ventas de un vendedor en un rango de fechas.  

### 1.4 Consultar inventario  
- Devuelve stock actual de productos.  

### 1.5 Generar reporte de ventas  
- Agrupa ventas por fecha, sucursal y vendedor.  

---

## 2. Triggers  

### 2.1 Actualizar inventario  
- Disminuye stock al insertar en `Detalle_Venta`.  
- Aumenta stock si una venta es anulada.  

### 2.2 Registrar fecha de creación  
- Antes de insertar en `Usuarios`, asigna fecha actual.  

### 2.3 Validar sobreventa  
- Antes de insertar en `Detalle_Venta`, calcula `sobreventa_codigo`.  

---

## 3. Vistas (Views)  

### 3.1 Vista_Ventas_Diarias  
- Muestra ventas por fecha, sucursal, vendedor y tipo.  

### 3.2 Vista_Comisiones  
- Muestra total de sobreventas, mitad almacén y mitad empleados.  

### 3.3 Vista_Nomina_Empleados  
- Une `Nomina_Diaria` con `Nomina_Empleados` para mostrar pagos diarios.  

### 3.4 Vista_Reporte_Ventas  
- Reporte diario, semanal y mensual filtrado por sucursal o vendedor.  

---
