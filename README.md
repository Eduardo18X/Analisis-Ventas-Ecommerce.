# Análisis de Rendimiento de Ventas - E-commerce 📊

Este proyecto simula el flujo de trabajo de un Analista de Datos en un entorno comercial. El objetivo es diseñar una base de datos relacional transaccional, extraer información estratégica mediante consultas y presentar los resultados finales en un reporte ejecutivo.

## 🛠️ Herramientas Utilizadas
* **SQL Server / MySQL:** Diseño del modelo relacional, inserción de registros y ejecución de consultas avanzadas (`JOINs`, `GROUP BY`).
* **Microsoft Excel:** Diseño del reporte comercial, ordenamiento de datos y visualización ejecutiva.

---

## 💻 Código SQL del Proyecto

A continuación, se detalla el script utilizado para la creación de la base de datos, las tablas relacionadas y las consultas analíticas de negocio:

```sql
-- 1. Creación de la base de datos ficticia para el análisis
CREATE DATABASE EcommerceDB;
USE EcommerceDB;

-- 2. Creación de la tabla de Productos
CREATE TABLE Productos (
    ProductoID INT PRIMARY KEY,
    NombreProducto VARCHAR(100),
    Categoria VARCHAR(50),
    Precio DECIMAL(10,2)
);

-- 3. Creación de la tabla de Ventas
CREATE TABLE Ventas (
    VentaID INT PRIMARY KEY,
    ProductoID INT,
    Cantidad INT,
    FechaVenta DATE,
    MontoTotal DECIMAL(10,2),
    FOREIGN KEY (ProductoID) REFERENCES Productos(ProductoID)
);

-- INSERCIÓN DE DATOS DE PRUEBA
INSERT INTO Productos VALUES 
(1, 'Laptop Core i7', 'Tecnología', 3200.00),
(2, 'Monitor 24 IPS', 'Tecnología', 750.00),
(3, 'Silla Ergonómica', 'Oficina', 450.00),
(4, 'Teclado Mecánico', 'Tecnología', 250.00);

INSERT INTO Ventas VALUES 
(101, 1, 2, '2026-05-10', 6400.00),
(102, 2, 1, '2026-05-11', 750.00),
(103, 3, 5, '2026-05-12', 2250.00),
(104, 1, 1, '2026-05-14', 3200.00),
(105, 4, 3, '2026-05-15', 750.00);

-- CONSULTAS REQUERIDAS POR EL NEGOCIO (RECLUTADORES)

-- Consulta A: Total de ventas agrupado por categoría de producto (Uso de INNER JOIN y GROUP BY)
SELECT p.Categoria, SUM(v.Cantidad) AS TotalUnidadesVendidas, SUM(v.MontoTotal) AS IngresosTotales
FROM Ventas v
INNER JOIN Productos p ON v.ProductoID = p.ProductoID
GROUP BY p.Categoria
ORDER BY IngresosTotales DESC;

-- Consulta B: Productos con ventas mayores a un monto específico (Uso de WHERE)
SELECT NombreProducto, Precio 
FROM Productos 
WHERE Precio >= 500.00;
