---
layout: post
title:  "Control de errores PL/SQL"
tags: Oracle Database
---
### Pequeña guia del Control de Errores

Error en PL/SQL:

```sql
PLSQL: ORA-01722 Error Message 
```

- Para que nuestro programa no se caiga, es necesario manejar cualquier error y mantener el control de nuestro trabajo. 

¿De qué forma podemos manejar las excepciones para controlar estos errores?

- Primero debemos tener presente el contenido de nuestra consulta y adelantarnos a posibles errores, en segundo lugar saber cuáles son los errores mas comunes, estos lo puedes encontrar en. A continuaicon un ejemplo de como manejar los errores en código.

```sql
EXEPTION
WHEN nombre_o_codigo_excepcion1 THEN sentencia(INSERT INTO, variable, mensaje, etc);
```

El formato en el siguiente ejemplo:

```sql
EXEPTION
WHEN NO_DATA_FOUND THEN v_mensaje:='No se encontraron datos';
WHEN TOO_MANY_ROWS THEN v_mensaje:='La sentencia retorna más de un dato';

INSERT INTO errores
VALUES(sequence.NEXTVAL, v_mensaje);
```