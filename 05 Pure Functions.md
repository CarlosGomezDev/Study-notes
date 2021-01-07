`2020-01-04, Pure Functions, 12:00`

Pure Function is a function that given the same input, always returns the same output, and it only uses the input provided without affecting anything external to it, it's basically analogous to a mathematical function function. A pure function also lack side-effects, meaning, it doesn't affect anything outside of it, and treats all inputs as immutable.

The reasons for this constrains is to build a function that is easy to use and test, since we can be sure we'll receive the same output given the same input, and it's also easier to refactor in the future if necessary.

Since a pure function can't affect anything outside of it, there's a need for impure functions, thus code can't be 100% pure, but it shouldn't be either. Develop with as many pure functions as possible, and keep impure functions to a minimum.

---

Pure Function es una función que cuando recibe el mismo input, siempre devuelve el mismo output, y solo trabaja con el input que recibió sin usar nada externo, básicamente es el análogo informático de una función matemática. Tampoco tiene ningún efecto secundario, es decir, no afecta nada fuera de sí misma y trata los inputs que recibió como inmutables.

La idea de estos limites es una función fácil de usar y testear, ya que es seguro que el mismo input siempre devuelve el mismo output, y es más fácil refactorizar en el futuro si fuera necesario.

Ya que la función pura no puede afectar nada fuera de sí misma, se necesitan funciones impuras, entonces el código nunca puede ser 100% puro, pero no debería serlo tampoco. La idea es desarrollar con funciones puras lo más posible, para mantener las funciones impuras al mínimo.
