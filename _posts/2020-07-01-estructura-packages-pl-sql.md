---
layout: post
title: "Estructura Packages en PL/SQL"
tags: Oracle Database
---


Cabecera del Package

```sql
--Package cabecera
CREATE [OR REPLACE] PACKAGE <pkgName> 
IS
   
  -- Declaraciones de tipos y registros públicas
  {[TYPE <TypeName> IS <Datatype>;]}
  
  -- Declaraciones de variables y constantes publicas
  -- También podemos declarar cursores
  {[<ConstantName> CONSTANT <Datatype> := <valor>;]}  
  {[<VariableName> <Datatype>;]}
  -- Declaraciones de procedimientos y funciones públicas

  {[FUNCTION <FunctionName>(<Parameter> <Datatype>,...) 
    RETURN <Datatype>;]}
  {[PROCEDURE <ProcedureName>(<Parameter> <Datatype>, ...);]}
END <pkgName>;
```

Cuerpo del Package

```sql
CREATE [OR REPLACE] PACKAGE BODY <pkgName> 
IS
   
  -- Declaraciones de tipos y registros privados
  {[TYPE <TypeName> IS <Datatype>;]}
  
  -- Declaraciones de variables y constantes privadas
  -- También podemos declarar cursores
  {[<ConstantName> CONSTANT <Datatype> := <valor>;]}  
  {[<VariableName> <Datatype>;]}
  -- Implementacion de procedimientos y funciones 
  FUNCTION <FunctionName>(<Parameter> <Datatype>,...) 
  RETURN <Datatype> 
  IS
    -- Variables locales de la funcion
  BEGIN
    -- Implementeacion de la funcion
    return(<Result>);
  [EXCEPTION]
    -- Control de excepciones
  END;
  
  PROCEDURE <ProcedureName>(<Parameter> <Datatype>, ...)
  IS 
   -- Variables locales de la funcion
  BEGIN
    -- Implementacion de procedimiento
  [EXCEPTION]
    -- Control de excepciones
  END;
END <pkgName>;
```

Ejemplo del Package:

  El siguiente ejemplo crea un paquete llamado *PKG_CONTABILIDAD*.

  Para crear la especificación del paquete:

```sql
CREATE OR REPLACE PACKAGE PKG_CONTABILIDAD 
IS
   
  -- Declaraciones de tipos y registros públicas
  TYPE Cuenta_contable IS RECORD
  (
    codigo_cuenta VARCHAR2(6),
    naturaleza    VARCHAR2(2) ,
    actividad     VARCHAR2(4) , 
    debe_haber    VARCHAR2(1)
  );
  
  -- Declaraciones de variables y constantes publicas
  DEBE  CONSTANT VARCHAR2(1) := 'D';
  HABER CONSTANT VARCHAR2(1) := 'D';
  ERROR_CONTABILIZAR EXCEPTION;
  -- Declaraciones de procedimientos y funciones públicas
  PROCEDURE Contabilizar (mes VARCHAR2) ;
  FUNCTION  fn_Obtener_Saldo(codigo_cuenta VARCHAR2) RETURN NUMBER;
END PKG_CONTABILIDAD;
```

 Aquí  sólo hemos declarado las variables y constantes, prototipado las funciones y procedimientos públicos . Es en el cuerpo del paquete cuando escribimos el código de los subprogramas *Contabilizar* y *fn_Obtener_Saldo*.

```sql
CREATE PACKAGE BODY PKG_CONTABILIDAD IS
 FUNCTION fn_Obtener_Saldo(codigo_cuenta VARCHAR2) 
 RETURN NUMBER 
 IS
   saldo NUMBER;
 BEGIN
        SELECT SALDO INTO saldo
        FROM SALDOS
        WHERE CO_CUENTA = codigo_cuenta;
        return (saldo);
 END;
 
 PROCEDURE Contabilizar(mes VARCHAR2) 
 IS
   CURSOR cDatos(vmes VARCHAR2) 
   IS
   SELECT * 
   FROM FACTURACION 
   WHERE FX_FACTURACION = vmes 
     AND PENDIENTE_CONTABILIZAR = 'S';
 
   fila cDatos%ROWTYPE;
 
 BEGIN
   OPEN cDatos(mes); 
     LOOP FETCH cDatos INTO fila; 
     EXIT WHEN cDatos%NOTFOUND;
     /* Procesamiento de los registros recuperados */
     END LOOP; 
   CLOSE cDatos;
 
 EXCEPTION
 WHEN OTHERS THEN 
   RAISE ERROR_CONTABILIZAR;
 END Contabilizar;
END PKG_CONTABILIDAD; 
```

Es posible modificar el cuerpo de un paquete sin necesidad de alterar por ello la especificación del mismo.

Los paquetes pueden llegar a ser programas muy complejos y suelen almacenar gran parte de la lógica de negocio.