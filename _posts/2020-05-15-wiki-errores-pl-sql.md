---
layout: post
title: "Tabla de errores - PL/SQL"
tags: Oracle Database
description: Una breve tabla con sus respectivas descripciones de oracle, normalmente este error ocurre en PL/SQL
---

### Excepciones del sistema nombrados son:

| CodError | Referencia | Descripción|
| --- | :---: | --- |
|```06530 ```| ACCESS_INTO_NULL  | Se ha intentado asignar valores a los atributos de un  objeto que no se ha inicializado.|
| ``` 06592 ```| CASE_NOT_FOUND  | Ninguna de las opciones en la cláusula WHEN de una sentencia CASE se ha seleccionado y no se ha definido la cláusula ELSE.|
 |```06531 ```| COLLECTION_IS_NULL| Se intentó asignar valores a una tabla anidad o varray aún no inicializada.|
|```06511``` | CURSOR_ALREADY_OPEN | Se intentó abrir un cursor que ya se encuentra abierto.|
|```00001```| DUP_VAL_ON_INDEX | Se intentó ingresar un valor duplicado en una columna(s definida(s como Clave Primaria o Unique en la tabla.|
|```01001``` | INVALID_CURSOR | Se ha intentado efectuar una operación no válida sobre un cursor.|
|```01722```| INVALID_NUMBER | La conversión de una cadena de caracteres a número ha fallado cuando esa cadena no representa un número válido.|
|```01017``` | LOGIN_DENIED  | Se ha conectado al servidor Oracle con un nombre de usuario o password inválido.|
|```01403``` |NO_DATA_FOUND |  Una sentencia SELECT no retornó valores o se ha referenciado a un elemento no inicializado en una tabla indexada.|
|```01012``` | NOT_LOGGED_ON |  El programa PL/SQL efectuó una llamada a la Base de Datos sin estar conectado al servidor Oracle.|
|```06501``` | PROGRAM_ERROR| PL/SQL tiene un problema interno.|
|```06500``` | STORAGE_ERROR PL/SQL |Se quedó sin memoria o la memoria está corrupta.|
|```06533``` | SUBSCRIPT_BEYOND_COUNT |Se ha referenciado un elemento de una tabla anidad o índice de varray mayor que el número de elementos de la colección.|
|```06532``` | SUBSCRIPT_OUTSIDE_LIMIT | Se ha referenciado un elemento de una tabla anidada o índice de varray fuera del rango (Ej. -1.|
|```01410```  |SYS_INVALID_ROWID| Fallo al convertir una cadena de caracteres a un tipo ROWID.|
|```00051```| TIMEOUT_ON_RESOURCE |Se excedió el tiempo máximo de espera por un recurso de Oracle.|
|```01422``` | TOO_MANY_ROWS |Una sentencia SELECT INTO retorna más de una fila.|
|```06502```| VALUE_ERROR| Ocurrió un error aritmético, de conversión o truncamiento. Por ejemplo, cuando se intenta almacenar un valor muy grande en una variable más pequeña.|
|```01476``` |ZERO_DIVIDE| El programa intentó hacer una división por cero. |










