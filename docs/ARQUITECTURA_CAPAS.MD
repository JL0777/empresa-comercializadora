# Arquitectura en Capas del Sistema de Ventas y Nómina

## Tecnologías Confirmadas
- Frontend: React.js + TailwindCSS  
- Backend: Node.js con Express  
- Base de Datos: MySQL (servidor en XAMPP)  
- Control de Versiones: Git + GitHub  

---

## 1. Capa de Presentación (Frontend)
- Implementada en React.js con TailwindCSS.
- Funcionalidades:
  - Registro de ventas.
  - Consulta de nómina.
  - Reportes y dashboards.
  - Panel de administración.
- Comunicación con backend vía **endpoints REST**.

---

## 2. Capa de Lógica de Negocio (Backend)
- Implementada en Node.js con Express.
- Funciones:
  - Registro de ventas (con/sin comisión).
  - Cálculo de sobreventas (códigos).
  - Distribución de 2% en ventas sin comisión.
  - Generación de nómina (base + comisiones).
  - Integración de ventas de locales y sublocales.
- Incluye seguridad con JWT o Passport.js.

---

## 3. Capa de Acceso a Datos
- Base de datos: MySQL (XAMPP).
- ORM: Sequelize.
- Componentes:
  - Procedimientos almacenados (nómina).
  - Triggers (auditoría).
  - Vistas (reportes).
- Garantiza integridad y consistencia de datos.

---

## 4. Capa de Persistencia (Base de Datos)
- Tablas:
  - Empleados
  - Ventas
  - Productos
  - Pagos (Nómina)
  - Sublocales
  - Auditoría
- Relaciones normalizadas para reportes y cálculos.

---

## 🔄 Flujo General
1. Empleado registra venta en **frontend (React)**.
2. Backend (Node.js + Express) procesa y guarda en MySQL.
3. Triggers y procedimientos actualizan métricas de nómina.
4. Administrador consulta reportes y nómina en el frontend.
5. Vistas SQL optimizadas alimentan dashboards y reportes.
