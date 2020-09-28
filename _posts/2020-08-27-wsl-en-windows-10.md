---
layout: post
title: "¿Cómo acceder a los archivos WSL en Windows 10?"
tags: Guias, Linux, W10
---

### Datos Importantes para acceder a los archivos Linux de WSL

- Solo se puede acceder cuando la distribución esta en ejecución , ya que el servidor de archivo( **[9 Filesystem Protocol](https://es.wikipedia.org/wiki/9P)** o **[Styx](https://es.wikipedia.org/wiki/9P)** ) se ejecuta en cada distribución .
- CMD no admite rutas UNC ya que los archivos de Linux se trata de la misma manera que al recurso de la red.
- Nunca trates de acceder a los archivos de la distro WSL dentro de la carpeta AppData ya que omite el uso del servidor y corres el riesgo de corromper la distro.

### Comencemos:

La primera forma es abriendo la distribución , en mi caso Ubuntu:

![image-20200827134429603](/assets/img/posts/image-20200827134429603.png)

En el Bash de Ubuntu pegamos lo siguiente:

```properties
explorer.exe .
```

Inmediatamente se Abriera el Explorer de Windows 10 con los archivos de la distribución:

![image-20200827140147972](/assets/img/posts/image-20200827140147972.png)

La segunda forma es dentro del Explorador de Windows 10 en la barra de direcciones:

![image-20200827141029628](/assets/img/posts/image-20200827141029628.png)

Ingresamos lo siguiente :

```properties
\\wsl$\Ubuntu
```

Y le damos Enter, nos saldría la raíz de la distribución:

![image-20200827141600681](/assets/img/posts/image-20200827141600681.png)

- Ahora tenemos dos formas para acceder a los archivos WSL en Windows 10.
