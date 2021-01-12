`2020-01-10, Functional Approach JS, 23:00`

### Functional Programming:
> Programming paradigm where programs are constructed by applying and composing functions. It is a declarative paradigm, where function definitions are trees of expression that each return a value, instead of a sequence of imperative statements that change the state of the program.

E.g. Lisp and Haskel, natively supported in JS.

Why? What problem is it solved?
OOP: `Java`, `C++`
Procedural: `C`

Taking a large number of complex ideas, and organizing them in a coherent way (goal similar to OOP)
- OOP: basic idea of objects and relationships of objects.
	- Interfaces, subclasses, constructors, public/private/protected data, accessors, mutators, method overriding
- Functional: precition of mathematical functions into programming
	- Small, self-contained, easily testable parts

| OOP/Procedural | Functional |
| :------------ | :------------ |
| Imperative | Declarative |
| "How" | "What" |
|  to make a house, need to <br> pour foundation, build 4 walls, <br>build the roof supported by the wall | foundation, 4 walls, roof |
| set x to 0, add 1st number to x, <br>repeat adding all number, <br>divide x by length of array | x is the sum of all <br>numbers in array, <br>divided by length of array |

#### Main Concepts
1. **Immutability** = usually variables can be assigned and reassigned (`var` and `let`), in functional programming we say variables are **defined** once and cannot be **redefined** (`const`), you would never redefine **Pi** to another value.
	- To *change* a variable, we *define* a new one with the updated values: `name = 'Carlos'`, `updatedName = name + ' Gomez'`
	- When a program has many variables changing constantly, it is difficult to track what state the program is in, and very hard to find bugs.
	- In functional programming we start with an immutable set of data as a single source of truth, and then use functions to combine this data piece by piece. The original data is always intact, and it's easier to track changes
2. **Separating funtions and Data**: in OOP, data and functions go together, functional programming keeps them separate, with objects for data and objects for functions.
	- For example, a ToDo list in OOP would have a `ToDoItem` class with items data, functions, and getters, and a TodoList class.
	- Functional programming keeps these separate, with objects for todo items, array for the todo list, and functions for each.
3. **First-class functions**: treat functions like objects, strings, integers. They only work with the input they receive, and don't influence any external states. These are called **pure functions**. Try to make as many pure functions as possible.
	- In OOP data and functions are different entities, you never create an array of functions, passing functions as arguments to other functions, return a function from a function, or combine functions.
	- In functional programming, treat functions like strings/numbers/dates.


#### Ensuring immutability: ESLint
Using `const` you cannot redefine variables, but you can redefine *object* properties, so a mutating array method like `reverse` can override the original array. Objects have the same issue.
- ESLint helps you catch stylistic erros in your code, like accidental mutations
- Multiple plugins can be applied to ESLint, we are going to use ESLint-plugin-immutable

####Functions that return functions
- **Blackbox**: function that gets an input, and return something different as output, without knowing how
	- A blackbox can return another blackbox
- When we define a function, it has access to the internal function of its parent
- High order function is a function that take other functions as arguments, or return functions

`2020-01-11`

#### JavaScript, the functional parts
- Avoid using mutative array methods directly like `push`, `pop`, `sort`, `reverse`.
	- There are work around using `slice`.
- `Node.js` modules like `ESLint` (and plugins for `ESLint` like `eslint-plugin-immutable`) help detecting these unintentional mutations in your code.

**1. Spread operator**: grab all elements of an object, or array, at once. E.g. `numbers = [1,2,3,4,5]`, `...numbers` includes the whole array, spread operator can replace the mutative array method `push`.
```javascript
const person = {
    name: 'Jimmy Smith',
    age: 40,
    hairColor: 'brown',
    eyeColor: 'blue',
};
const updates = {
    name: 'Fake Name',

}
const updatedPerson = {
    ...person,
    ...updates,
}
console.log(updatedPerson);
/* {
  name: 'New Fake Name',
  age: 40,
  hairColor: 'brown',
  eyeColor: 'blue'
} */

const number = [1, 2, 3, 4, 5];
const newNumber = [
    ...number,
    6,
    9,
]
console.log(newNumber);
/* [
  1, 2, 3, 4,
  5, 6, 9
] */
```
**2. Map**: map is non-mutative method, so it is safe to use. Use it to apply a function to each array element.
```javascript
const numbers = [1, 2, 3, 4, 5];
const double = x => x * 2
const doubledNumber = numbers.map(double);
console.log(doubledNumber) //  [ 2, 4, 6, 8, 10 ]
```
**3. Filtering**, also non-mutative, takes a true/false for each element in array to decide if it should use or discard it.
```javascript
const wordsa = ['hello', 'goodbye', 'the', 'antartica'];
const lengthTest = minLength => wrd => wrd.length > minLength;
const longWords = wordsa.filter(lengthTest(5));
console.log(longWords); //[ 'goodbye', 'antartica' ]
```
**4. Every / Some**: compare every element to a logic expression, every returns true if all elements returned true, some returns true if at least 1 element returned true, and the opposite for false
```javascript
const employees = [{
    name: 'Jane Doe',
    salary: 90000,
}, {
    name: 'Donald Jones',
    salary: 65000,
}, {
    name: 'Donna Appleseed',
    salary: 1500000,
}, {
    name: 'John Smith',
    salary: 250000,
}];
const moreThanMillion = employees.every(sal => sal.salary >= 1000000); //true
const moreThanMillion = employees.every(sal => sal.salary >= 10000000); //false
const moreThanMillion = employees.every(sal => sal.salary >= 1000000); //false
const moreThanMillion = employees.every(sal => sal.salary >= 100); //true
```
**5. Slicing**: `slice` is not mutative, is not a high-order function, it does not take a function as an argument, but it has its uses.
- `Slice` expects two parameters, start and end.
