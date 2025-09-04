# **¿Que es una base de datos?**
+ Un conjunto de datos relacionados entre si, estructurados de forma que pueden ser consultados y modificados facilmente.
+ Un sistema organizado para almacenar, gestionar y recuperar informacion de manera eficiente.
+ Permite realizar operacion como busqueda, insercion y eliminacion de datos.
+ **Es un conjunto de datos pertenecientes a un mismo contexto almacenados sistematicamente para su posterior uso, si algunos datos que yo tengo cumplen con estos 4 criterios, puedo decir que es una base de datos.**
+ Por ejemplo una biblioteca, ya que es (un conjunto de datos) - (en un mismo contexto) - (almacenados sistematicamente) - (para su posterior uso).
# **¿Que no es una base de datos?**
+ Un archivo de texto sin estructura definida como un documento word o un archivo de notas suelto.
+ Una hoja de calculo simple (como Excel) puede parecerse a una base de datos, pero no ofrece las capacidades de gestion, integridad y consulta de una DBMS {(Database managment system) o (Gestor de sistema de datos) como por ejemplo: MariaDB, MYSQL, etc.}.
+ Un conjunto de datos sin relacion, estructura ni organizacion logica.
+ Un simple almacenamiento de informacion desordenada o sin un proposito de consulta estructurada.
# **Datos**
+ No dice nada por si solo.
+ No tiene relacion con nada.
+ Asi como:
  + 23
  + 180 (puede ser altura, peso, temperatura,...)
  + "Rojo"
# **Informacion**
+ Es una combinacion de datos.
+ Conclusiones.
+ Proyecciones.
+ **Es el conjunto de datos procesados, organizados y contextualizados de manera que tengan significado y valor para quien lo recibe**.
+ Asi como:
  + "Juan tiene 23 años".
  + "La camiseta es roja".
# **¿Que es persistencia de datos o en bases de datos?**
+ Persistencia significa que la informacion guardada sigue existiendo despues de cerrar el programa, apagar la computadora o reiniciar el sistema.
+ Es lo contrario a datos temporales.
+ Estas son las principales:
  + Memoria.
  + Archivos(planos, binarios).
  + Bases de datos.
+ Un ejemplo podria se hacer un back up en un DBMS.
# **Memoria**
## Memoria rapida
+ Puede o no borrarse.
+ Asi como cuando abres ventanas en el computador y lo que estas haciendo se te guarda aunque cambies de ventana.
+ Se guarda en el cache o en cpu.
## Memoria volatil
+ RAM.
+ Se pierde facilmente o no se guarda cuando no hay energia.
+ Siempre se borra.
# **Tipos de archivos**
## Archivos planos
+ Pueden leerse independientemente del lenguaje de programacion.
+ Permite usar formatos estandares (xml,json,..,etc.).
+ Legibilidad, se puede leer.
## Archivos binarios
+ Implica serializar los objetos.
+ Puede estar ligado a un formato, como (jpg,exe,etc.).
+ Un ejemplo es cuando tu tomas una foto ese archivo es uno binario.
## Ambos presentan lo siguiente:
+ Posibles problemas de concurrencia. **Osea son errores que ocurren cuando múltiples procesos/usuarios acceden o modifican los mismos datos simultáneamente sin coordinación adecuada.**
+ Posibles datos duplicados.
+ Poca integridad de los datos. **Osea es cuando los datos no son confiables porque están incorrectos, incompletos, inconsistentes o han sido alterados de forma indebida.**
  + Ejemplo de datos alterado:
    + Datos incorrectos/imposibles:
      + Edad: -5 años
      + Temperatura: 500°C en una habitación
      + Fecha: 2025-13-45 (mes 13, día 45)
      + Email: usuario@@@@mail..com
      + Precio: $-100
    + Datos incompletos:
      - Campos obligatorios vacíos (nombre, ID)
      - Registros a medias por cortes de proceso
      - Referencias rotas (pedido sin cliente)
    + Inconsistencias.
    + Duplicados indebidos.
    + Datos desactualizados.
+ Poca o nula correlacion entre los datos. **Osea es cuando los datos no se pueden relacionar o cruzar entre sí de manera útil, ya sea por problemas técnicos o porque realmente no tienen conexión lógica.**
  + ❌ Poca correlación:
    + Sensor temperatura: {id: "T001", valor: 25, time: "15:30"}.
    + Sensor humedad: {code: "HUM-A1", reading: 65, timestamp: 1634567890}.
    + Sensor presión: {sensor: "barometer_01", data: 1013, fecha: "14/08"}.
    
    1) Imposible saber si están en el mismo lugar.
    2) No puedo calcular índice de confort (temp+humedad).
    3) Formatos de tiempo diferentes.
  
  + ✅ Buena correlación:
    + {sensor_id: "LAB_001_TEMP", ubicacion: "LAB_001", valor: 25, timestamp: "2025-08-14T15:30:00Z"}.
    + {sensor_id: "LAB_001_HUM", ubicacion: "LAB_001", valor: 65, timestamp: "2025-08-14T15:30:00Z"}.
    
    1) Mismo lugar (LAB_001), mismo momento.
    2) Puedo calcular índices combinados.
# **La base de datos**
+ Maneja concurrencia.
+ Permite varias conexiones al mismo tiempo.
+ Permite evitar duplicidad de datos.
+ Manejo tipo de datos, por ende su integridad.
+ Permite correlacionar los datos y convertirlos en informacion.
+ Se puede tener historia de los datos y sus cambios.
## Clasificaciones de una base de datos
+ **SQL o relacional: Las bases de datos relacionales se llaman así porque las tablas se relacionan unas con otras através de claves comunes, permitiéndote hacer consultas que cruzan información entre múltiples tablas.**
## Ejemplos de si son o no BD
+ Si:
  + Conjunto de libros en una biblioteca.
  + Lista de mercado.
  + Lista de contactos en un celular.
  + Un horario de clases.
  + Lista de cosas por hacer.
  + Seguidores en redes sociales.
+ No:
  + Excel.
  + Firebase.
  + Oracle.
  + Mysql.
  + Estos son DBMS y no BD.
# **Glosario**
+ Query: Consulta o pregunta que le haces a una base de datos para obtener, modificar o manipular información.
+ Registro: Una fila completa en una tabla de base de datos que representa una instancia específica de una entidad.
+ Tabla: Una estructura organizada que almacena datos en filas y columnas, como una hoja de cálculo de Excel, pero en una base de datos.
+ Campos: Una columna en una tabla que define un tipo específico de información que se puede almacenar.(id,codigo,tipo,ubicacion,activo,etc.).
+ Big Data: Conjuntos de datos tan grandes, complejos o que crecen tan rápido que las herramientas tradicionales de bases de datos no pueden procesarlos eficientemente.
