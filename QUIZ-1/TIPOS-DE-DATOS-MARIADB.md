````markdown name=Resumen-examen-modelado-datos.md
# Tipos de datos en MariaDB
(Numéricos, decimales exactos, flotantes y textos, con sintaxis, criterios de identificación y ejemplos “a mano”.)



============================================================
Numéricos (enteros) — visión general
============================================================

- Qué son
  - Valores sin parte decimal: 0, 1, 2, 3, … (y, si aplica, negativos).
  - Se usan para contar, enumerar o identificar sin decimales.

- Señales para identificarlos en un enunciado
  - “cantidad”, “unidades”, “stock”, “ítems”, “edad”, “número de asiento”, “piso”, “intentos”, “puntuación entera”.
  - Ejemplos de valores: 0, 7, 15, 120 (sin “coma” o “punto” decimal).

- Sintaxis (columna)
  - TIPO [UNSIGNED] [NOT NULL] [DEFAULT valor]

- Nota práctica en examen (sin memorizar rangos)
  - Elige un tipo más pequeño si el enunciado sugiere “pocos” valores (p.ej., edades, pisos).
  - Elige un tipo más grande para conteos más altos o identificadores generales.



============================================================
TINYINT — ejemplo y cómo reconocerlo
============================================================

- Qué es (para valores enteros muy pequeños)
  - Útil para cantidades muy acotadas, banderas/estados numéricos o edades.

- Cómo lo identificar en el enunciado
  - Edad, número de intentos, nivel (0–5), calificación de 0 a 10 en entero, piso (0–50).

- Ejemplos de valores
  - edad: 0, 7, 15, 98
  - intentos: 0, 1, 2, 3
  - nivel: 1, 2, 3, 4, 5

- Ejemplo de columna (sintaxis)
  - edad TINYINT UNSIGNED
  - intentos TINYINT UNSIGNED DEFAULT 0

- Mini-tabla (dibujada)
  | Campo    | Tipo sugerido         |
  |----------|------------------------|
  | id       | INT (PK)               |
  | edad     | TINYINT UNSIGNED       |
  | intentos | TINYINT UNSIGNED       |



============================================================
SMALLINT — ejemplo y cómo reconocerlo
============================================================

- Qué es (para enteros pequeños/medianos)
  - Cantidades que pueden llegar a “cientos” o “miles” razonables.

- Cómo lo identificar en el enunciado
  - Asientos de una sala, cantidad de ítems en un pedido, stock moderado.

- Ejemplos de valores
  - asientos: 120, 250, 500
  - cantidad: 1, 5, 30, 200

- Ejemplo de columna (sintaxis)
  - asientos SMALLINT UNSIGNED
  - cantidad SMALLINT UNSIGNED DEFAULT 0

- Mini-tabla
  | Campo     | Tipo sugerido           |
  |-----------|--------------------------|
  | id_sala   | INT (PK)                 |
  | asientos  | SMALLINT UNSIGNED        |
  | numerada  | TINYINT UNSIGNED         |



============================================================
MEDIUMINT — ejemplo y cómo reconocerlo
============================================================

- Qué es (para enteros de rango intermedio)
  - Cuando el enunciado sugiere “miles” o “decenas/cientos de miles” de registros o conteos.

- Cómo lo identificar en el enunciado
  - Visitantes anuales de un parque, número de tickets emitidos en una temporada.

- Ejemplos de valores
  - visitantes: 12_500, 85_000, 300_000

- Ejemplo de columna (sintaxis)
  - visitantes_anuales MEDIUMINT UNSIGNED

- Mini-tabla
  | Campo              | Tipo sugerido            |
  |--------------------|---------------------------|
  | id_parque          | INT (PK)                  |
  | visitantes_anuales | MEDIUMINT UNSIGNED        |



============================================================
INT — ejemplo y cómo reconocerlo
============================================================

- Qué es (entero “general” de uso común)
  - Para identificadores, conteos habituales y datos enteros en general.

- Cómo lo identificar en el enunciado
  - id de tablas, stock de productos con alta rotación, número de facturas.

- Ejemplos de valores
  - id: 1, 2, 3, …; stock: 1_500; facturas: 12_345

- Ejemplo de columna (sintaxis)
  - id INT NOT NULL
  - stock INT UNSIGNED DEFAULT 0

- Mini-tabla
  | Campo    | Tipo sugerido   |
  |----------|------------------|
  | id       | INT (PK)         |
  | stock    | INT UNSIGNED     |
  | activo   | TINYINT UNSIGNED |



============================================================
BIGINT — ejemplo y cómo reconocerlo
============================================================

- Qué es (para enteros muy grandes)
  - Identificadores o contadores que pueden crecer mucho (muchísimos registros).

- Cómo lo identificar en el enunciado
  - id de sistemas con altísimo volumen, contador global acumulado.

- Ejemplos de valores
  - id_registro: 9_000_000, 25_000_000, …

- Ejemplo de columna (sintaxis)
  - id BIGINT NOT NULL
  - contador BIGINT UNSIGNED

- Mini-tabla
  | Campo     | Tipo sugerido     |
  |-----------|--------------------|
  | id        | BIGINT (PK)        |
  | contador  | BIGINT UNSIGNED    |



============================================================
Decimales exactos (numéricos con decimales) — DECIMAL(p, s)
============================================================

- Qué son
  - Números con decimales exactos (sin aproximación); típicos de dinero y totales precisos.

- Señales para identificarlos
  - “precio”, “importe”, “total”, “saldo”, “tasa exacta”.

- Ejemplos de valores
  - 19.99, 250.00, 0.15

- Sintaxis (columna)
  - DECIMAL(p, s) [NOT NULL] [DEFAULT valor]

- Ejemplos de columna
  - precio DECIMAL(10,2) NOT NULL
  - impuesto DECIMAL(5,2) DEFAULT 0.00

- Mini-tabla
  | Campo   | Tipo sugerido  |
  |---------|-----------------|
  | id      | INT (PK)        |
  | precio  | DECIMAL(10,2)   |
  | impuesto| DECIMAL(5,2)    |



============================================================
Flotantes (aproximados) — FLOAT / DOUBLE
============================================================

- Qué son
  - Números con decimales “aproximados” (para mediciones físicas, sensores).

- Señales para identificarlos
  - “peso”, “temperatura”, “humedad”, “medición”.

- Ejemplos de valores
  - 1.75, 0.85, 23.10

- Sintaxis (columna)
  - FLOAT [NOT NULL] [DEFAULT valor]
  - DOUBLE [NOT NULL] [DEFAULT valor]

- Ejemplos de columna
  - peso FLOAT
  - temperatura DOUBLE

- Mini-tabla
  | Campo       | Tipo sugerido |
  |-------------|---------------|
  | id          | INT (PK)      |
  | peso        | FLOAT         |
  | temperatura | DOUBLE        |



============================================================
Textos (recordatorio)
============================================================

- Tipos
  - CHAR(n): longitud fija
  - VARCHAR(n): longitud variable
  - TEXT: texto largo (observaciones, descripciones amplias)

- Señales para identificarlos
  - Códigos alfanuméricos, nombres, descripciones, notas.

- Ejemplos de columna
  - codigo CHAR(10)
  - nombre VARCHAR(100)
  - descripcion TEXT



============================================================
Diagnóstico rápido en examen (a mano)
============================================================

- ¿Tiene decimales?
  - Sí y debe ser exacto → DECIMAL(p, s)
  - Sí pero es medición aproximada → FLOAT/DOUBLE
  - No → entero (TINY/SMALL/MEDIUM/INT/BIGINT según magnitud sugerida por el enunciado)

- ¿Puede ser negativo?
  - No → UNSIGNED
  - Sí → con signo (por defecto)

- ¿Es dinero?
  - Usa DECIMAL (no flotante)

- ¿Es un id con muchísimos registros?
  - Usa INT o BIGINT según el caso descrito.



============================================================
Ejercicios de identificación “rápidos”
============================================================

1) “Edad de persona”, valores: 0, 7, 15, 98
- Tipo: TINYINT UNSIGNED

2) “Cantidad en carrito”, valores: 0, 1, 2, …, 500
- Tipo: SMALLINT UNSIGNED

3) “Visitantes anuales” del parque, valores: 12_500; 85_000; 300_000
- Tipo: MEDIUMINT UNSIGNED

4) “Id de pedido” en un sistema general
- Tipo: INT (PK)

5) “Id de registro” en un sistema con altísimo volumen
- Tipo: BIGINT (PK)

6) “Precio de venta”, valores: 3.50, 12.00, 1599.99
- Tipo: DECIMAL(p, s) (por ejemplo, DECIMAL(10,2))

7) “Peso (kg)”, valores: 1.75, 0.50, 23.10
- Tipo: FLOAT (o DOUBLE según detalle del enunciado)
