`2020-01-12, Function Declaration vs Expression`

### Functions in Javascript
Every JavaScript function is a `function` object.
By default, functions return `undefined`, unless a return statement is specified.
Declared Functions as `hoisted` so they can be used in a line before they are declared, but that is not the case with Function Expressions.
Functions can have default values for their parameters.


```javascript
hoisted(); // logs "foo"

function hoisted() {
  console.log('foo');
}
notHoisted(); // TypeError: notHoisted is not a function

var notHoisted = function() {
   console.log('bar');
};

//Default parameters value in arrow function
(a=400, b=20, c) => expression
```

#### Function Declaration
Also called Function Statement, defines a function and its parameters with the `function` keyword.
A function can be conditionally declared, meaning it can be nested within an `if` statement, but results are inconsistent and should not be used in production code, function expressions are preffered.

```javascript
function name([param[, param,[..., param]]]) {
   [statements]
}
```


#### Function Expression
Using the 'function' keyword to define a function inside an expression. Funtion Expressions are not hoisted.
- Very similar to Function Declarations, except `function name` is optional, this created *anonymous* functions.
  - If the name is ommited, the variable the function is assigned too will be its *implicit* name, on the contrary if a name is declared, it will be an *explicit* name.
    - Arrow functions in contrast do not have an *explicit* name, so they can only have an *implicit* name
  - Function Expressions can also be used as *Immediately Invoked Function Expressions*, which run as soon as they defined/expressed.

```javascript
//unammed
var x = function(y) {
   return y * y;
};
//callback
button.addEventListener('click', function(event) {
    console.log('button is clicked!')
})
//IIFE
(function() {
    console.log('Code runs!')
})();
```

#### Arrow Functions
- Compact version of traditional function expression, but have some limits and cannot be used in all situations.
  - Do not have their own bindings to `this` or `super`, and should not be used as `methods`.

```javascript
// Traditional Function
function (a){ return a + 100};
// 1. Remove the word "function" and place arrow
(a) => {return a + 100};
// 2. Remove the body brackets and word "return" as it is implied if function only has one expression
(a) => a + 100;
// 3. Remove the argument parentheses if only one argument
a => a + 100;
//We can also treat them as variables
let bob = a => a + 100;
//To return an object, we need parethesis
a => ({foo: "a"})
```

#### Inmediately Invoked Function Expression (IIFE)
Also known as Self-Executing Anonymous Function
Runs as soon as it is defined, and it has two parts:
1. The anonymous function enclosed with `Grouping Operator ()`
2. The function invocation with `()`, through which the JavaScript engine will interpret the anonymous function in part 1.

```javascript
(function () {
    statements
})();

(function () {
    var aName = "Barry";
})();
// Variable aName is not accessible from the outside scope
aName // throws "Uncaught ReferenceError: aName is not defined"
```

Assigning the IIFE to a variable stores the function's return value, not the function definition itself.

```javascript
var result = (function () {
    var name = "Barry";
    return name;
})();
// Immediately creates the output:
result; // "Barry"
```