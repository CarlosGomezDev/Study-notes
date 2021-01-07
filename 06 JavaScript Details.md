`2020-01-06, JavaScript Detail, 14:00`

HTML > Tag > Attribute = Value > textNode or another Tag

- ES6 always use updates

  - `Const` and `Let`
  - Destructuring
    - `const player = obj.player`
      vs
    - `const { player } = obj;`
  - New dynamic object properties (imagine const name = "John Snow")
    - `const obj = { name: 'hello'};` //that is equal to name: hello
      vs
    - `const object = { [name]: 'hello'}` // equal to John Snow = hello
  - Template strings
    - `"Hello" + name + ", how are you?"`
      vs
    - `` `Hello ${name}, how are you?` ``
  - Default Argument
    - Function parameters can have default values
    - `Function myFunction (para1, para2)`
      vs
    - `Function myFunction(para1 = 1, para2 = 'abc')`
  - Arrow functions
    - ` Function myFunction(a , b){ return a * b; }`
    - Vs
    - `Const myFunction = (a, b) => a * b;`

- Expression = fragment of code that produces a value
- Functions = pieces of code that perform an action
  - function > return
  - function expressions can be anonymous (no name)
  - () mean execute function
  - Examples:
    - `alert()`
    - `prompt()`
    - Custom `function()`
- Arguments = values given to functions and methods
- Paramaters = optional values the function is expecting to receive
- Methods = functions inside an object
  - 1st party integrated into JS itself or 3rd by yourself as developer
- Index = order of items inside arrays
- Expression = piece of code that produces a value
- Calling / Invoking a function = using () after function name
- Closures = a child function scope has access to parent function scope, but not global scope
  - Parent function doesn't have access to child scope
- Currying = changing a function with multiple parameters to take only 1 parameter at a time
  - `const multiple => (a, b) => a * b;`
    vs
  - `const curriedMultiple => (a) => (b) => a * b`
  - `const multiplyBy5 = curriedMultiply(5)` // a is now locked to 5
    • multiplyBy5(10) // this reads a locked as 5, and sets b as 10 = 50
- Side-effects = actions that happen inside a function that affect anything outside of it
- Purity = avoid side effects, and always return something to avoid undefined
- Deterministic = if my inputs are always the same, my output is always the same.
- Imperative vs Declarative, jQuery vs React.js
- Synchronous vs Asynchronous
  - Synchronous: Running call stack in order vs in any order
  - Asynchronous: using setTimeout to defer instructions
- Single threaded language that can be non-blocking (with async)
- JavaScript events vs HTML attribute events
- Try to avoid .innerHTML because it re-parses the whole DOM
  - You want to minimize DOM manipulation and re-draws
- JavaScript engine (e.g.: Chrome - V8)
  - Memory Heap
  - Call stack
- Compose = putting two functions together, where the output of 1 function is the input of another function
  - Seems to be a function that contains multiple functions and can call all of those in a chain, needs more research

![](https://raw.githubusercontent.com/CarlosGomezDev/Study-notes/main/src/img/02-1.png)

- Calling / Invoking a method = object.functionInsideObject
- Callback function = function that is called after a condition is met or event is triggered
- Function declaration
  function functionName(){
  functionCodeHere;
  }
- Function Expression
  const variableName = function(){
  functionCodeHere;
  }
