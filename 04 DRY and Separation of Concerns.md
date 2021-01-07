`2021-01-02, DRY and Separation of Concerns, 23:00`

#### DRY & Separation of Concern <br>

###### DRY - Dont Repeat Yourself - No te repitas <br>

Concepto viene del libro "The Pragmatic Programmer", donde se toca el tema de la repetición de información y sus consecuencias. El autor expresa que la única manera de desarrollar software de manera confiable, y facilitar el entendimiento y mantenimiento de ese software, es seguir el principio DRY: <br>

> Cada pieza de información debe ser representada dentro de un sistema de manera unitaria, inequívoca, y autoritaria. Lo contrario sería tener la misma información expresada en dos o más lugares, si una cambia, debes recordar cambiar las demás.

La finalidad es reducir la repetición de patrones de software, y en su lugar utilizar abstracciones y normalización de data.
Se puede tomar como ejemplo el tema del conocimiento en código, y conocimiento en comentarios. Los comentarios deben ser explicaciones de alto nivel, el **por qué** de una implementación, su propósito y finalidad, mientras que el código en si debe ser una explicación de bajo nivel, el **cómo** de una implementación. Un comentario que explique el **cómo **estaría duplicando conocimiento, e inevitablemente tendremos que actualizar uno cuando cambie el otro.
¿Como surge la repetición de información?

- Repetición impuesta: los desarrolladores sienten que no tiene otra opción, el requerimiento aparente obligar a la duplicación
- Repetición inadvertida: los desarrolladores no se dan cuentan que están duplicado información.
- Repetición impaciente: los desarrolladores duplican información por pereza o por aparentar ser el camino más fácil.
- Repetición entre desarrolladores: varias personas de un equipo o diferentes equipos duplican información.

###### Separation of Concerns - Separación de Intereses <br>

Es una forma de abstracción que siga la estrategia de dividir y conquistar. Se basa en dividir un problema en dos o mas sub-problemas, hasta que son lo suficientemente sencillos para resolverlos directamente. Esto permite libertad en el diseno, implementacion, mantenimiento, y uso de una programa.
En programación, se logra con:

- Modularization de codigo, separarando y encapsulando funcionalidades en modulos independientes e intercambiables, cada uno con la programacion necesaria para ejecutar un aspecto de una funcionalidad
- Diseno orientado a objectos, planificando un sistema de interacciones de objectos con la finlidad de solucionar un problema de programacion.

La finalidad es poder entender, diseñar, y manejar sistemas interdependientes complejos, y poder reusar y optimizar funciones de manera independente.

Un ejemplo de separación de intereses es la relación entre HTML, CSS, y JavaScript. HTML se encarga de organizar los elementos de la página web, CSS se encarga de definir el estilo y presentación de esos elementos, y JavaScript se encarga del comportamiento de los elementos y la interacción con el usuario.
