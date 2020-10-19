---
layout: post
title: "Patrones de Diseño"
tags: Software
description: Patrones de Diseño en Desarrollo Software
---

Los Patrones se clasifican en 3 Grupos:

- Patrón creacional - Patrón estructural - Patrón de comportamiento

### Patrón creacional

Son los que **facilitan la tarea de creación de nuevos objetos**, de tal forma que el proceso de creación pueda ser desacoplado de la implementación del resto del sistema.

Patrones creacionales más conocidos son:

- **Abstract Factory**: Nos provee una interfaz que delega la creación de un conjunto de objetos relacionados sin  necesidad de especificar en ningún momento cuales son las implementaciones concretas .
- **Factory Method**: Expone un método de creación, delegado en las subclases la implementación de este método.
- **Builder**: Separa la creación de un objeto complejo de su estructura, de tal forma que el mismo proceso de construcción nos puede servir para crear representaciones diferentes.
- **Singleton**: Limita a uno el número de instancias posibles de una clase en nuestro programa, y proporciona un acceso global al mismo.
- **Prototype**: Permite la creación de objetos basados en "plantillas". Un nuevo objeto se crea a partir de la clonación de otro objeto.

### Patrón estructural

Son patrones que nos **facilitan el modelamiento de nuestro software**, especificando la forma en la que las clases se relacionan una con otras.

Patrones estructurales más conocidos son:

- **Bridge**: Desacopla una abstracción de su implementación, para que las dos puedan evolucionar de forma independiente.
- **Adapter**: Permite a dos clases con diferentes interfaces trabajar entre ellas, a través de un objeto intermedio con el que se comunican e interactúan.
- **Composite**: Facilita la creación de estructuras de objetos en árbol, donde todos los elementos emplean una misma interfaz,.cada uno de ellos puede a su vez contener listado de esos objetos, o ser el ultimo de esa rama.
- **Decorator**: Permite añadir funcionalidad extra a un objeto(de forma dinámica o estática) sin modificar el comportamiento del resto de objetos del mismo tipo.
- **Facade**: Es un objeto que crea una interfaz simplificada para tratar con otra parte del código más compleja, de tal forma que simplifica y asila su uso. Un ejemplo podría ser crear una fachada para tratar con una librería externa.
- **Flyweight**: Una gran cantidad de objetos comparte un mismo objeto con propiedades comunes con el fin de ahorrar memoria.
- **Proxy**: Es una clase que funciona como interfaz hacia cualquier otra cosa: una conexión a internet, un archivo en disco o cualquier otro recurso que sea costoso o imposible de duplicar. 

### Patrón de comportamiento

En este último grupo se encuentran la mayoría de los patrones y se usan para gestionar algoritmos, relaciones y responsabilidades entre objetos.

Los patrones de comportamiento más conocidos son:

- **Command**: Son objetos que encapsulan una acción y los parámetros que necesitan para ejecutarse.
- **Chain of responsibility**: Se evita acoplar al emisor y receptor de una repetición dado la posibilidad  a varios receptores de consumirlo. Cada receptor tiene la opción de consumir a esa petición o pasárselo al siguiente dentro de la cadena.
- **Interpreter**: Define una representación para una gramática, así como el mecanismo para evaluarla. El árbol de sintaxis del lenguaje suele modelar mediante el  patrón composite.
- **Iterator**: Se utiliza para poder movernos por los elementos de un conjunto de forma secuencial sin necesidad de exponer su implementación especifica.
- **Mediator**: Objeto que encapsula como otro conjunto de objetos interactúa y se comunican entre si.
- **Observer**: Los objetos son capaces de suscribirse a una serie de eventos que otro objetivo va a emitir, y serán avisados cuando esto ocurra.
- **State**: Permite modificar la forma en que un objeto se comporta en tiempo de ejecución, basándose en su estado interno.
- **Strategy**: Permite la elección del algoritmo que ejecuta cierta acción en tiempo de ejecución.

​					

