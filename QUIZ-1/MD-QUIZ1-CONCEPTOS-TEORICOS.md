````markdown name=Resumen-examen-modelado-datos.md
# Modelo de Datos — Resumen para examen
(Notas detalladas “tipo noticia”, solo con lo visto en las diapositivas:
Conceptos generales, Tipos de datos y PK, MER y Normalización. Incluye ejemplos.)



============================================================
01) Glosario esencial
============================================================

- Integridad
- Correlación
- Conjunto de datos
- Entidad
- Relaciones
- Tipos de datos
- Numéricos (MariaDB)
- Flotantes
- Textos
- Clave primaria (PK)
- Modelo relacional
- MER (Modelo Entidad–Relación)
- Normalización (1FN, 2FN, 3FN)



============================================================
02) Conceptos generales
============================================================

- Conjunto de datos
  - Es un grupo de datos relacionados y organizados.
  - Ejemplo: una tabla “Clientes” con todas las filas de clientes es un conjunto de datos.

- Entidad
  - Objeto del mundo real del que se guarda información.
  - Ejemplo: Cliente, Producto, Pedido.

- Relaciones
  - Asociación entre entidades.
  - Cardinalidades típicas: 1:1, 1:N, N:M.
  - Ejemplo: “Cliente realiza Pedido” (Cliente 1:N Pedido).

- Correlación
  - Asociación observable entre datos (no implica causalidad).
  - Ejemplo: “más pedidos, más puntos acumulados”.

- Integridad
  - Reglas para mantener los datos correctos y coherentes.
  - Ejemplo: no permitir claves primarias duplicadas o nulas.

- Modelo relacional
  - Entidades → tablas.
  - Atributos → columnas.
  - Relaciones → claves (PK/FK) y tablas de unión en N:M.



Ejemplo rápido (conceptos)
- Entidad: Producto(id, nombre, precio)
- Relación: Cliente 1:N Pedido (un cliente puede tener muchos pedidos)
- Integridad: la columna id de Producto es única y no nula (PK)



============================================================
03) Tipos de datos (MariaDB) y PK
============================================================

- Numéricos (enteros)
  - TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT
  - Sintaxis (columna): TIPO [UNSIGNED] [NOT NULL] [DEFAULT valor]
  - Uso: contadores, cantidades, identificadores “numéricos”.
  - Ejemplos:
    - cantidad SMALLINT UNSIGNED DEFAULT 0
    - id INT NOT NULL

- Decimales exactos (numéricos con decimales)
  - DECIMAL(precision, escala)
  - Uso: montos, precios (valores exactos).
  - Ejemplos:
    - precio DECIMAL(10,2) NOT NULL
    - impuesto DECIMAL(5,2) DEFAULT 0.00

- Flotantes (aproximados)
  - FLOAT, DOUBLE
  - Uso: mediciones aproximadas (p. ej., peso, temperatura).
  - Ejemplos:
    - peso FLOAT
    - temperatura DOUBLE

- Textos
  - CHAR(n): longitud fija
  - VARCHAR(n): longitud variable
  - TEXT: texto largo
  - Ejemplos:
    - codigo CHAR(10) NOT NULL
    - nombre VARCHAR(100)
    - descripcion TEXT

- Clave primaria (PK)
  - Identifica de forma única cada fila.
  - Debe ser única y no nula.
  - Puede ser un identificador (id) o un dato natural del negocio si es único y estable.

Ejemplo (tipos + PK, sintaxis MariaDB)
```sql
CREATE TABLE productos (
  id INT NOT NULL,
  nombre VARCHAR(100) NOT NULL,
  precio DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (id)
);
```



============================================================
04) MER (Modelo Entidad–Relación)
============================================================

- Entidades y atributos
  - Entidad: “Cliente”, “Pedido”, “Producto”.
  - Atributos: “Cliente.nombre”, “Pedido.fecha”, “Producto.precio”.

- Relaciones y cardinalidad
  - 1:1, 1:N, N:M.
  - N:M se resuelve con una tabla intermedia al pasar a tablas.

- Atributos especiales (tratamiento)
  - Compuestos: se pueden descomponer (dirección → calle, número, ciudad).
  - Multivaluados: se modelan en tabla aparte (ClienteTelefono).
  - Derivados: se calculan (ej.: edad desde fecha_nacimiento).

Ejemplo (MER → tablas)
- Cliente 1:N Pedido
  - Tablas:
    - Cliente(id, nombre)
    - Pedido(id, fecha, cliente_id)
  - Pedido.cliente_id referencia a Cliente.id.

- Pedido N:M Producto
  - Tablas:
    - Producto(id, nombre, precio)
    - DetallePedido(pedido_id, producto_id, cantidad)
  - DetallePedido relaciona el pedido con sus productos.



============================================================
05) Normalización (1FN, 2FN, 3FN)
============================================================

- 1FN (Primera Forma Normal)
  - Celdas atómicas (sin listas ni grupos repetidos).
  - Mal: Cliente(telefonos = '111,222')
  - Bien:
    - Cliente(id, nombre)
    - ClienteTelefono(cliente_id, telefono)

- 2FN (Segunda Forma Normal)
  - Si la PK es compuesta, cada atributo no clave depende de toda la clave (no de una parte).
  - Mal: Detalle(pedido_id, producto_id, nombre_producto)
  - Bien:
    - Producto(id, nombre)
    - Detalle(pedido_id, producto_id, cantidad)

- 3FN (Tercera Forma Normal)
  - Ningún atributo no clave depende de otro no clave (sin dependencias transitivas).
  - Mal: Cliente(codigo_postal, ciudad) si “codigo_postal → ciudad”
  - Bien:
    - Cliente(id, nombre, codigo_postal)
    - (Opcional) Catálogo CP–ciudad, o no duplicar “ciudad” si depende del CP.



============================================================
06) Ejemplos integrales (de enunciado a modelo)
============================================================

A) Tienda (Cliente, Pedido, Producto)
- Entidades:
  - Cliente(id, nombre)
  - Pedido(id, fecha, cliente_id)
  - Producto(id, nombre, precio)
- Relaciones:
  - Cliente 1:N Pedido
  - Pedido N:M Producto → DetallePedido(pedido_id, producto_id, cantidad)
- Normalización aplicada:
  - 1FN: sin listas en columnas.
  - 2FN: “nombre_producto” no va en Detalle, pertenece a Producto.
  - 3FN: evitar duplicar datos que dependan de otros no clave.

B) Universidad (Alumno, Curso)
- Entidades:
  - Alumno(id, nombre)
  - Curso(id, nombre)
- Relación:
  - N:M → Inscripcion(alumno_id, curso_id, fecha)



============================================================
07) Cómo analizar un caso en el examen
============================================================

- Extrae entidades (sustantivos) y atributos del enunciado.
- Determina relaciones y cardinalidades (1:1, 1:N, N:M).
- Define PK para cada entidad (única, no nula).
- Asigna tipos de datos coherentes (numéricos, decimales, flotantes, textos).
- Verifica:
  - 1FN: sin listas ni campos combinados.
  - 2FN: en PK compuesta, nada depende de solo una parte.
  - 3FN: sin dependencias transitivas entre no claves.
- Si hay N:M, crea la tabla intermedia.



============================================================
08) “Qué no se cumple / qué está mal” (patrones y corrección)
============================================================

- 1FN violada
  - Listas en una columna (teléfonos unidos por comas).
  - Corrección: tabla hija (ClienteTelefono).

- N:M sin tabla intermedia
  - IDs múltiples en una columna.
  - Corrección: tabla Detalle/Inscripción.

- 2FN/3FN violadas
  - Atributos en la tabla equivocada (dependen de un componente de la PK o de otro no clave).
  - Corrección: moverlos a su entidad correspondiente.



============================================================
09) Preguntas tipo examen (alineadas a las diapositivas)
============================================================

- Define: Entidad, Relación, Conjunto de datos, Modelo relacional (con un ejemplo).
- Distingue: numéricos, decimales exactos y flotantes; y textos en MariaDB (con sintaxis).
- ¿Qué es la PK? Define una PK para dos tablas de un caso.
- Identifica cardinalidades 1:1, 1:N, N:M en un enunciado y mapea a tablas.
- Detecta y corrige violaciones a 1FN, 2FN y 3FN en un esquema propuesto.
````
````markdown name=tipos-datos-mariadb.md
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
````
