---
layout: post
title: "Estructura Procedimiento Almacenados en PL/SQL"
tags: Oracle Database
description: Estructura Procedimientos Almacenados..
---


```sql
CREATE [OR REPLACE} PROCEDURE [esquema].nombre-procedimiento 
(nombre-parametro {IN | OUT | IN OUT} tipo de dato, ..) {IS | AS} 

​	Declaracion de variables;
​	Declaracion de constantes; 
​	Declaracion de cursores; 
BEGIN 
​	Cuerpo del subprograma PL/SQL;

​	EXCEPTION 
​	Bloque de excepciones PL/SQL; END;

END;
```


Ejemplo Procedimiento Almacenado:

1.  OBJETIVO: guardar información de ventas a clientes en una tabla

```sql
CREATE TABLE reg_errores(
    sec_error NUMBER(5) PRIMARY KEY,
    subprograma VARCHAR2(50) NOT NULL,
    mensaje VARCHAR2(200) NOT NULL
);
```

Cuando no especifico el START WITH y el INCREMENT BY,
por defecto es 1

```sql
CREATE SEQUENCE seq_errores;
```



```sql
CREATE TABLE informe_venta(
    anio VARCHAR2(6) NOT NULL,
    cliente_id NUMBER NOT NULL,
    nombre_cliente VARCHAR2(60) NOT NULL,
    cantidad_ventas NUMBER NOT NULL,
    cantidad_de_productos NUMBER NOT NULL,
    valor_neto NUMBER NOT NULL,
    iva NUMBER NOT NULL,
    descuento NUMBER NOT NULL,
    total_boleta NUMBER NOT NULL
);
```

 Creo mi procedimiento

```sql
CREATE OR REPLACE PROCEDURE sp_informe_ventas IS
    CURSOR cur_informe_ventas IS
    SELECT TO_CHAR(fecha,'MMYYYY') AS "anio",
           c.cliente_id,
           c.nombre_cia,
           COUNT(b.nro_boleta) AS "cantidad_ventas",
           SUM(cantidad) AS "cantidad_productos",
           SUM(valor_neto) AS "neto",
           SUM(iva) AS "iva",
           NVL(SUM(b.descuento),0) AS "descuento",
           SUM(total) AS "total"
    FROM boletas b
    INNER JOIN ordenes o
        ON b.orden_id=o.orden_id
    INNER JOIN clientes c
        ON o.cliente_id=c.cliente_id
    INNER JOIN detalle_ordenes d
        ON o.orden_id=d.orden_id
    GROUP BY TO_CHAR(fecha,'MMYYYY'), c.cliente_id, c.nombre_cia;
    

    reg_informe_ventas cur_informe_ventas%ROWTYPE;
    v_mensaje VARCHAR2(200);


BEGIN
    --desarrollo de un cursor
    OPEN cur_informe_ventas;
        LOOP
            FETCH cur_informe_ventas INTO reg_informe_ventas;
            EXIT WHEN cur_informe_ventas%NOTFOUND;
            BEGIN
                --guardar los datos
                INSERT INTO informe_venta VALUES(reg_informe_ventas."anio",
                                                 reg_informe_ventas.cliente_id,
                                                 reg_informe_ventas.nombre_cia,
                                                 reg_informe_ventas."cantidad_ventas",
                                                 reg_informe_ventas."cantidad_productos",
                                                 reg_informe_ventas."neto",
                                                 reg_informe_ventas."iva",
                                                 reg_informe_ventas."descuento",
                                                 reg_informe_ventas."total");
                                                 
            EXCEPTION
            WHEN OTHERS THEN
                v_mensaje:=SQLERRM || ' - ' || SQLCODE;
                INSERT INTO reg_errores VALUES(seq_errores.NEXTVAL,
                                               'sp_informe_ventas',
                                               v_mensaje);
        	END;
    	END LOOP;
    CLOSE cur_informe_ventas;

--alternativa: CUANDO EL SELECT QUEDA IGUAL QUE LA TABLA DESTINO
/*FOR x IN cur_informe_ventas LOOP
    BEGIN
        --MAYOR TRUCO DE LA VIDA
        INSERT INTO informe_venta VALUES x;
        
        EXCEPTION
        WHEN OTHERS THEN
            v_mensaje:=SQLERRM || ' - ' || SQLCODE;
            INSERT INTO reg_errores VALUES(seq_errores.NEXTVAL,
                                               'sp_informe_ventas',
                                               v_mensaje);
    END;
END LOOP;*/

END sp_informe_ventas;

--ejecuto mi procedimiento
EXECUTE sp_informe_ventas;
```

 2. Creo mi tabla paramétrica

```sql
CREATE TABLE rango_subida_comision(
    id_rango NUMBER(5) PRIMARY KEY,
    inicio NUMBER(15) NOT NULL,
    fin NUMBER(15) NOT NULL,
    porcentaje NUMBER(15) NOT NULL
);
```

```sql
insert into RANGO_SUBIDA_COMISION values(1,1,1200,15);
insert into RANGO_SUBIDA_COMISION values(2,1201,2300,20);
insert into RANGO_SUBIDA_COMISION values(3,2301,3500,25);
insert into RANGO_SUBIDA_COMISION values(4,3501,4500,30);
insert into RANGO_SUBIDA_COMISION values(5,4501,6500,35);
insert into RANGO_SUBIDA_COMISION values(6,6501,8900,40);
insert into RANGO_SUBIDA_COMISION values(7,8901,20000,45);
insert into RANGO_SUBIDA_COMISION values(8,20001,40000,50);
insert into RANGO_SUBIDA_COMISION values(9,40001,400000000,50);
```

```sql
Create table informe_subida_comision
(mes_annio_informe varchar2(6) NOT NULL,
 ID_EMPLEADO NUMBER NOT NULL,
 NOMBRE_COMPLETO varchar2(40) NOT NULL,
 COMISION number NOT NULL,
 SUELDO_ACTUAL number NOT NULL, 
 PORCENTAJE_SUB number NOT NULL,
 NUEVA_COMISION number NOT NULL
 );
```

```sql
CREATE OR REPLACE PROCEDURE sp_comisiones(p_contador OUT NUMBER,
                                          p_mensaje OUT VARCHAR2) IS
    CURSOR cur_comision IS
    SELECT TO_CHAR(fecha_comision,'MMYYYY') AS "mes_anio",
           e.empleado_id,
           e.nombre || ' ' || e.apellido AS "nombre_completo",
           SUM(c.valor_comision) AS "comision",
           e.sueldo
    FROM comisiones c
    INNER JOIN empleados e
        ON c.empleado_id=e.empleado_id
    GROUP BY TO_CHAR(fecha_comision,'MMYYYY'), e.empleado_id, e.nombre,
                e.apellido, e.sueldo;
    
v_porcentaje NUMBER;
v_nueva_comision NUMBER;

BEGIN
    p_contador:=0;
    FOR x IN cur_comision LOOP
        --NECESITO CALCULAR EL PORCENTAJE Y LA NUEVA COMISION
        SELECT porcentaje
        INTO v_porcentaje
        FROM rango_subida_comision
        WHERE x."comision" BETWEEN inicio AND fin;
        
    v_nueva_comision:=(1+(v_porcentaje/100))*x."comision";
    v_nueva_comision:=ROUND(v_nueva_comision);
    
    INSERT INTO informe_subida_comision VALUES(x."mes_anio",
                                               x.empleado_id,
                                               x."nombre_completo",
                                               x."comision",
                                               x.sueldo,
                                               v_porcentaje,
                                               v_nueva_comision);
    	p_contador:=p_contador+1;
    END LOOP;
END sp_comisiones;
```

Ejecuto mi procedimiento

 > NOTA: Siempre que un procedimiento me entregue valores... NECESITO UN PEQUEÑO BLOQUE

```sql
SET SERVEROUTPUT ON;
```

```sql
DECLARE
    v_contador NUMBER;
    v_mensaje VARCHAR2(100);
BEGIN
    /*el procedimiento almacenado me devuelve al parametro contador, y yo lo debo
    almacenar en una variable, para poder utilizarlo como necesite*/
    sp_comisiones(v_contador, v_mensaje);
    DBMS_OUTPUT.put_line('El total de empleados con comisiones es ' || v_contador);
END;
```

