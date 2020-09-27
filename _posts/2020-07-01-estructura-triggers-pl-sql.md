---
layout: post
title: "Estructura Triggers en PL/SQL"
tags: Oracle Database
---
Los disparadores son eventos a nivel de tabla que se ejecutan automáticamente cuando se realizan ciertas operaciones sobre la tabla.

```sql
CREATE {OR REPLACE} TRIGGER nombre_disp
  [BEFORE|AFTER]
  [DELETE|INSERT|UPDATE {OF columnas}] [ OR [DELETE|INSERT|UPDATE {OF columnas}]...]
  ON tabla
  [FOR EACH ROW [WHEN condicion disparo]]
[DECLARE]
  -- Declaración de variables locales
BEGIN
  -- Instrucciones de ejecución
[EXCEPTION]
  -- Instrucciones de excepción
END;
```


|   Orden de Disparo    |   :old    |   :new    |
|   :---: |   :---:   |   :---:     |
|   INSERT  |   No definido; todos los campos toman el valor NULL.           |   Valores que serán insertados cuandose complete la orden |
|   UPDATE  |   Valores originales de la fila, antes de la actualización.    |	Nuevos valores que serán escritoscuando se complete la orden.   |
|   DELETE  |   Valores originales, antes del borrado de la fila.            |   No definido; todos los campos tomanel valor NULL.   |

