````markdown name=Resumen-examen-modelado-datos.md
# Banco de ejercicios “a mano” — Modelo de Datos
Basado en lo visto en las diapositivas: Conceptos generales, Tipos de datos (numéricos, flotantes, textos), PK, MER y Normalización (diapositiva 06 con ejemplos).  
Formato pensado para examen escrito: enunciados, tablas “dibujadas”, identificar forma normal, integridad y tipos de datos.  
Incluye ejercicios fáciles e intermedios/no tan intuitivos, con soluciones al final.



============================================================
## A) Ejercicios FÁCILES (nivel 1)
============================================================

1) 1FN (atomicidad de atributos)
Tabla “Cliente” (propuesta del enunciado):
| id | nombre        | telefonos     |
|----|---------------|---------------|
| 1  | Ana Martínez  | 111,222       |
| 2  | Luis Pérez    | 333           |

Tareas:
- Indica si está en 1FN. ¿Por qué?
- Proponé una corrección a tablas.



2) 2FN (dependencia de toda la PK compuesta)
Tablas (propuesta del enunciado):
- Pedido(id, fecha, cliente_id)
- Detalle(pedido_id, producto_id, nombre_producto, cantidad)

Tareas:
- Indica si “Detalle” cumple 2FN. ¿Por qué?
- Proponé una corrección a columnas/tablas.



3) 3FN (dependencia transitiva)
Tabla “Cliente”:
| id | nombre        | codigo_postal | ciudad     |
|----|---------------|---------------|------------|
| 1  | Ana Martínez  | 28001         | Madrid     |
| 2  | Luis Pérez    | 08001         | Barcelona  |

Tareas:
- ¿Está en 3FN? Explica brevemente.
- Propón una alternativa que respete 3FN.



4) Tipos de datos (MariaDB: numéricos, flotantes, textos)
Para cada columna, di qué tipo corresponde (entero/decimal/flotante/texto) según los valores:

- cantidad = 5, 10, 12
- precio = 19.99, 250.00
- peso = 1.75, 0.85, 2.10
- codigo = “AB1234”
- descripcion = “Producto en oferta” (texto libre)

Tareas:
- Asigna el tipo general (entero / decimal exacto / flotante / texto).
- Si algún dato te parece mal ubicado, explícalo.



============================================================
## B) Ejercicios INTERMEDIOS (nivel 2)
============================================================

5) Integridad de entidad y referencial
Tablas y datos:
Tabla “Cliente”
| id | nombre        |
|----|---------------|
| 10 | Ana Martínez  |

Tabla “Pedido”
| id | fecha       | cliente_id |
|----|-------------|------------|
| 50 | 2025-03-10  | 10         |
| 51 | 2025-03-11  | 99         |  ← Cliente 99 no existe

Tareas:
- ¿Se cumple la integridad de entidad y referencial?
- Marca el problema y su corrección.



6) MER a tablas (1:N)
Enunciado: “Un Profesor imparte muchos Cursos. Cada Curso es impartido por exactamente un Profesor. Cada Curso puede tener 0..N Exámenes.”

Tareas:
- Identifica entidades y relaciones (con cardinalidades).
- Lista las tablas resultantes (nombres de columnas y PK).



7) MER a tablas (N:M con atributo de relación)
Enunciado: “Un Alumno puede inscribirse en muchos Cursos, y un Curso tiene muchos Alumnos. De la inscripción se guarda la fecha.”

Tareas:
- Indica la cardinalidad.
- Diseña las tablas y claves (sin escribir SQL).



8) Atributo compuesto y multivaluado
Enunciado:
- La Sucursal guarda “dirección” (calle, número, ciudad).
- Un Cliente puede tener varios correos electrónicos.

Tareas:
- Propón las tablas/columnas para representar ambos casos cumpliendo 1FN.



============================================================
## C) Ejercicios NO TAN INTUITIVOS (nivel 3)
============================================================

9) PK (elección y coherencia)
Enunciado: “Producto” trae un “codigo_barras” (ej.: “7791234567890”) que es único por producto.  
Tabla propuesta:
| codigo_barras | nombre        | precio  |
|---------------|---------------|---------|
| 779...890     | Cepillo       | 2.50    |

Tareas:
- ¿Podría “codigo_barras” ser PK? Justifica con lo visto (unicidad, no nulo).
- Menciona una alternativa de PK válida para “Producto” si no usas el código.



10) 3FN (dependencia transitiva escondida)
Tabla “Clase”:
| id_clase | curso_id | aula_id | capacidad_aula |
|----------|----------|---------|----------------|

Regla (implícita en el dominio):
- aula_id → capacidad_aula (la capacidad depende del aula)

Tareas:
- ¿Viola 3FN? Explica por qué.
- Propón una organización de tablas/columnas que respete 3FN.



11) 2FN (atributo que depende de parte de la clave)
Tabla “Inscripcion”
| alumno_id | curso_id | carrera  | fecha      |
|-----------|----------|----------|------------|

Regla del dominio:
- “carrera” depende del alumno (cada alumno pertenece a una carrera), no de la combinación alumno-curso.

Tareas:
- ¿Viola 2FN? Explica.
- Indica dónde debe residir “carrera”.



12) Tipos y ubicación (trampa con formatos)
Tabla “Promo”
| id | porcentaje_descuento | precio_base | etiquetas          |
|----|----------------------|-------------|--------------------|
| 1  | “12,5%”              | 100.00      | “hogar,cocina”     |

Tareas:
- Clasifica el tipo de dato de cada columna (entero/decimal/flotante/texto).
- ¿Ves violaciones a 1FN o problemas de dominio? ¿Cómo lo corregirías?



13) Participación (obligatoriedad de relación)
Enunciado: “Todo Pedido debe tener al menos un Detalle.”  
Datos:
Tabla “Pedido”:
| id_pedido | fecha       |
|-----------|-------------|
| 200       | 2025-04-01  |
| 201       | 2025-04-02  |

Tabla “Detalle”:
| pedido_id | producto_id | cantidad |
|-----------|-------------|----------|
| 201       | 5           | 1        |

Tareas:
- ¿Se cumple la participación indicada por la regla?
- Señala el problema y cómo lo detectarías/corregirías en el diseño.



14) N:M mal resuelta “a ojo”
Tabla “Alumno”
| id | nombre | curso1 | curso2 | curso3 |
|----|--------|--------|--------|--------|
| 1  | Ana    | BD     | POO    |        |

Tareas:
- Explica por qué esto viola 1FN y no representa N:M.
- Propón el esquema correcto.



============================================================
## D) SOLUCIONES RESUMIDAS
============================================================

1) 1FN
- No cumple 1FN: “telefonos” contiene múltiples valores en una sola celda.
- Corrección:
  - Cliente(id, nombre)
  - ClienteTelefono(cliente_id, telefono)  (una fila por cada número)



2) 2FN
- No cumple 2FN: en Detalle la PK es (pedido_id, producto_id) y “nombre_producto” depende solo de “producto_id”.
- Corrección:
  - Producto(id, nombre, precio, …)
  - Detalle(pedido_id, producto_id, cantidad)



3) 3FN
- Si “codigo_postal → ciudad”, entonces “ciudad” depende de un no-clave (CP), es dependencia transitiva y viola 3FN.
- Alternativas:
  - Guardar solo “codigo_postal” en Cliente y obtener “ciudad” en consulta, o
  - Mantener un catálogo CP–Ciudad y referenciarlo (según el caso).



4) Tipos
- cantidad: numérico entero.
- precio: decimal exacto (numérico con decimales).
- peso: flotante (medición aproximada).
- codigo: texto (por ejemplo, alfanumérico).
- descripcion: texto (libre).



5) Integridad
- Integridad de entidad: OK si las PK no son nulas/duplicadas.
- Integridad referencial: incumplida (pedido 51 apunta a cliente 99 inexistente).
- Corrección: asegurar que cliente_id apunte a un id existente o eliminar ese registro inconsistente.



6) MER 1:N (Profesor–Curso) y 1:N (Curso–Examen)
- Entidades: Profesor, Curso, Examen.
- Relaciones:
  - Profesor 1:N Curso (cada Curso tiene 1 Profesor).
  - Curso 0..N Examen.
- Tablas (columnas de ejemplo y PK):
  - Profesor(id_profesor, nombre, …)
  - Curso(id_curso, nombre, id_profesor)
  - Examen(id_examen, fecha, id_curso)



7) MER N:M (Alumno–Curso) con atributo en la relación
- Cardinalidad: N:M.
- Tablas:
  - Alumno(id_alumno, nombre, …)
  - Curso(id_curso, nombre, …)
  - Inscripcion(id_alumno, id_curso, fecha)



8) Compuesto y multivaluado
- Dirección compuesta: Sucursal(id, calle, numero, ciudad).
- Emails multivaluados: Cliente(id, nombre); ClienteEmail(id_cliente, email).



9) PK “codigo_barras”
- Puede ser PK si es único y no nulo (cumple definición de PK).
- Alternativa: un id numérico (id_producto) como PK y mantener “codigo_barras” con restricción de unicidad.



10) 3FN en “Clase”
- Viola 3FN: “capacidad_aula” depende de “aula_id”, no de la PK de Clase.
- Corrección:
  - Aula(aula_id, capacidad)
  - Clase(id_clase, curso_id, aula_id)   (y capacidad se obtiene por aula_id)



11) 2FN en “Inscripcion”
- Viola 2FN: PK compuesta (alumno_id, curso_id) y “carrera” depende de alumno_id (parte de la PK).
- Corrección: “carrera” debe estar en la entidad Alumno.



12) Tipos y 1FN en “Promo”
- Tipos esperables:
  - porcentaje_descuento: debería ser numérico (decimal), no texto con “%”.
  - precio_base: decimal exacto.
  - etiquetas: viola 1FN (lista en una celda).
- Corrección:
  - porcentaje_descuento como número (ej.: 12.5).
  - Tabla PromoEtiqueta(id_promo, etiqueta) para una por fila.



13) Participación “todo Pedido con al menos un Detalle”
- No se cumple: el pedido 200 no tiene filas en Detalle.
- Corrección: asegurar la regla en el proceso/diseño (control de negocio); en evaluación manual, detectarlo revisando que cada pedido tenga al menos un detalle.



14) N:M mal resuelta
- Viola 1FN (múltiples cursos en columnas) y no representa N:M.
- Esquema correcto:
  - Alumno(id, nombre)
  - Curso(id, nombre)
  - AlumnoCurso(id_alumno, id_curso) (una fila por relación)



============================================================
## E) MINI-GUÍA “QUÉ MIRAR” EN CADA EJERCICIO
============================================================

- 1FN: ¿hay listas en una columna? ¿atributos compuestos sin descomponer?
- 2FN: si hay PK compuesta, ¿algún atributo depende solo de una parte?
- 3FN: ¿algún no-clave determina a otro no-clave (dependencia transitiva)?
- PK: ¿única y no nula? ¿elegida coherentemente con el dominio?
- Integridad referencial: ¿valores “hijos” existen en la “tabla padre”?
- Cardinalidad: ¿1:1 / 1:N / N:M está bien representada? ¿N:M con tabla intermedia?
- Tipos de datos (MariaDB): entero, decimal exacto, flotante, texto — ¿coinciden con los valores?
