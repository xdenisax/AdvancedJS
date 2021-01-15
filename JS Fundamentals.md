# Advanced JavaScript Concepts

### Global Execution Context
- the place where code is run in JS
- first context created
- first item added to callstack
- holds *Global Object* and *this*
- multiple scripts combine their global execution contexts into a big global one

### Lexical Environment
- context where the code is written 

### Variable environment
- holds the variables attached to execution context

### Hoisting 
- part of creation phase
- elevates variables and function to the top of the context

- **variables** are *partially* hoisted
    - it is allocated memory for the variable, but the value is set to undefined
- **function declarations** are *fully* hoisted
    - the content of the function is also stored in memory
- **function expressions** are *partially* hoisted 
    - they are treated as variables and stored with the value of undefined

### Function invocation
- made with ()
- it creates an **execution context** on top of *Global Execution Context/ parent Context*
- it creates a local **this** and **arguments**
- **arguments** = object holding the values of parameters => handy when you don't want to access each parameter and want to parse them using a loop
- parameters can be received by destructuring the object into an array
```function a(...args) {}```

### Scope chain 
- gives **access** to variables that are **in the parent environment**.
- used when a variable is **not** found in the **variable environment**. In this case, using the *scope chain*, the variable is searched in the **parent environment**. 

### Scope types
- **block scope** - defined by any {}
- **function scope** - defined by {} of a function

### Variable declarations 
- **const** = constants
- **let** = not available outside the block scope, neither outside the function scope
- **var** = available outside the block scope, but not outside the function scope

### Scope
- visibility of variables
- function based
- where the function is invoked
- where the function is in variable environment

### Context 
- object based 
- where this points

### IIFE
- **I**mmediately **I**nvoked **F**unction **E**xpression
- executed immediately after it is declared - variables can't be access from the outside environment

### this
- holds the object the function is property of
- gives methods  access to their object siblings
- can execute same function for multiple objects
- dynamically scoped =>
    - **inside an usual function**:
     it is bound to the environment that called the function, not to the environment where is written in (not in lexical environment)
    - **inside an arrow function**:
    opposite to usual function
    arrow function binds this to the environment where it is written, not the environment that calls the function

### call(), apply(), bind()
- **call()** gives an object the power to lend its methods to other objects
``` obj1.method.call(ob2, param1, param2)```
- **apply()** behaves like *call()*, but instead of individual params, it gets an array of params
``` obj1.method.apply(ob2, [param1, param2])```
- **bind()** bahves like *call() and apply()*, but it doesn't run the function, it ***returns*** the function to be used later on
``` obj1.method.bind(ob2, param1, param2)```


