# Endpoints REST - Sistema de Ventas y Nómina

---

## 1. Autenticación y Usuarios
- `POST /api/auth/login` → Iniciar sesión
- `POST /api/auth/register` → Registrar usuario
- `GET /api/usuarios` → Listar usuarios
- `GET /api/usuarios/:id` → Ver un usuario
- `PUT /api/usuarios/:id` → Actualizar usuario
- `DELETE /api/usuarios/:id` → Eliminar usuario

---

## 2. Productos e Inventario
- `GET /api/productos` → Listar productos
- `POST /api/productos` → Crear producto
- `PUT /api/productos/:id` → Editar producto
- `DELETE /api/productos/:id` → Eliminar producto
- `PATCH /api/productos/:id/stock` → Actualizar stock

---

## 3. Ventas
- `POST /api/ventas` → Registrar venta
- `GET /api/ventas` → Listar ventas
- `GET /api/ventas/:id` → Ver venta específica
- `GET /api/ventas/empleado/:id` → Ventas por empleado
- `GET /api/ventas/fecha/:fecha` → Ventas por fecha

---

## 4. Nómina
- `POST /api/nomina/calcular` → Calcular nómina del día
- `GET /api/nomina/:fecha` → Consultar nómina diaria
- `GET /api/nomina/empleado/:id` → Ver pago de un empleado

---

## 5. Reportes
- `GET /api/reportes/ventas` → Reporte de ventas consolidadas
- `GET /api/reportes/nomina` → Reporte de nómina
- `GET /api/reportes/sucursal/:id` → Reporte por sucursal o sublocal
