2020-01-04, Pure Functions, 12:00

Pure Function es una función que cuando recibe el mismo input, siempre devuelve el mismo output, y solo trabaja con el input que recibió sin usar nada externo, básicamente es el análogo informático de una función matemática. Tampoco tiene ningún efecto secundario, es decir, no afecta nada fuera de sí misma y trata los inputs que recibió como inmutables.

La idea de estos limites es una función fácil de usar y testear, ya que es seguro que el mismo input siempre devuelve el mismo output, y es más fácil refactorizar en el futuro si fuera necesario.

Ya que la función pura no puede afectar nada fuera de sí misma, se necesitan funciones impuras, entonces el código nunca puede ser 100% puro, pero no debería serlo tampoco. La idea es desarrollar con funciones puras lo más posible, para mantener las funciones impuras al mínimo.
