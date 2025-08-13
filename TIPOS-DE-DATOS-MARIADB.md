# Tipos de datos en MariaDB
(Numéricos, decimales exactos, flotantes y textos, con sintaxis y ejemplos.)



============================================================
Numéricos (enteros)
============================================================

- Tipos comunes
  - TINYINT
  - SMALLINT
  - MEDIUMINT
  - INT
  - BIGINT

- Sintaxis (columna)
  - TIPO [UNSIGNED] [NOT NULL] [DEFAULT valor]

- Ejemplos
  - id INT NOT NULL
  - cantidad SMALLINT UNSIGNED DEFAULT 0
  - existencias BIGINT

Ejemplo (tabla)
```sql
CREATE TABLE inventario (
  id INT NOT NULL,
  producto_id INT NOT NULL,
  cantidad SMALLINT UNSIGNED DEFAULT 0,
  PRIMARY KEY (id)
);
```



============================================================
Decimales exactos (numéricos con decimales)
============================================================

- Tipo
  - DECIMAL(precision, escala)   -- por ejemplo DECIMAL(10,2)

- Sintaxis (columna)
  - DECIMAL(p, s) [NOT NULL] [DEFAULT valor]

- Ejemplos
  - precio DECIMAL(10,2) NOT NULL
  - impuesto DECIMAL(5,2) DEFAULT 0.00

Ejemplo (tabla)
```sql
CREATE TABLE productos (
  id INT NOT NULL,
  nombre VARCHAR(100) NOT NULL,
  precio DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (id)
);
```



============================================================
Flotantes (aproximados)
============================================================

- Tipos
  - FLOAT
  - DOUBLE

- Sintaxis (columna)
  - FLOAT [NOT NULL] [DEFAULT valor]
  - DOUBLE [NOT NULL] [DEFAULT valor]

- Ejemplos
  - peso FLOAT
  - temperatura DOUBLE

Ejemplo (tabla)
```sql
CREATE TABLE mediciones (
  id INT NOT NULL,
  peso FLOAT,
  temperatura DOUBLE,
  PRIMARY KEY (id)
);
```



============================================================
Textos
============================================================

- Tipos
  - CHAR(n)        -- longitud fija
  - VARCHAR(n)     -- longitud variable
  - TEXT           -- texto largo

- Sintaxis (columna)
  - CHAR(n) [NOT NULL] [DEFAULT valor]
  - VARCHAR(n) [NOT NULL] [DEFAULT valor]
  - TEXT [NOT NULL]

- Ejemplos
  - codigo CHAR(10) NOT NULL
  - nombre VARCHAR(100)
  - descripcion TEXT

Ejemplo (tabla)
```sql
CREATE TABLE clientes (
  id INT NOT NULL,
  codigo CHAR(10) NOT NULL,
  nombre VARCHAR(100) NOT NULL,
  notas TEXT,
  PRIMARY KEY (id)
);
```
