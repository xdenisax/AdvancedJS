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
- creates a scope that doesn't allow variables to leak outside in parent scope and maybe overwrite something

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

### Object.freeze() 
- will create an entire immutable object
- trying to update object properties won't throw an error, but won't change the object either

**Note**: 
    - const objects can have properties updated, but not itself 
    - frozen object (built with Object.freeze()) won't have this behaviour
    
### Arrow function & this
- arrow functions see the this as the object parent
``` 
const button = document.querySelector('.button');
button.addEventListener('click', function() { // function is used here because we need to use the this as the button 
                                        // if we had arrow function here, the this would ve been the parent object (in this case window)
    this.classList.toggle('opening');
    setTimeout(()=> {   //arrow function is used here because we need the this to the parent object in this case the button
                        // if we used function here, the this would ve been undefined
        this.classList.toggle('open');
    })
})
```
- ***Don't use arrow functions:***
    - as parameter functions (exemple above)
    - as method in objects
        ``` const person = {
                name: 'defuault', 
                callName: () => { //this won't work, because this arrow function will point to the parent object
                                    // use function instead or directly: callname() {} <- shorthand
                    console.log(this.name)
                }
            }
        ```
    - binding functions to prototypes of the classes 
        ``` class Car { ... } 
            Car.prototype.summarize = () => { // won't work because this will point to the parent (in this case the window object)
                                            // use Car prototype.summarize = function() {} instead
                console.log('car info')    
            }
         ```
    - when ```arguments``` object is needed
     
#### Template strings
    are used for: 
- multiple lines
- looping through objects
- running functions inside 

### Destructuring
- spread object by properties  
    ``` const person = { 
            name: "Ann", 
            birthDate: { 
                day: 10,
                month: "Dec", 
                year: 1998
                }
            }
            const { day: d, month: m, year: y } = person.birthDate; //day - property as found in object, d - variable to store the day in
        
    ```
- spread arrays 
    ``` const person = 'Ann, 10, 12, 1998';
        cont [name, day, month, year] = person.split(','); 
    ```
- rest operator 
    ``` const person = ['Ann', 10, 12, 1998];
        const [ name, ...date ] = person;
    ```

### Loops
- ***for in*** -> loops through everything inside the object, including the prototype 
- ***for of*** -> loops only through elements of the iterable (arrays, strings, dom nodes, document objects, map, sets)
- ***using ```entries()```***
    ``` 
        for (const [i,cut] of cuts.entries()) {
            console.log(i, cut);
         }
    ````

### Array functtions
   exemple of nonArrayVector: arguments
   - Array.from() - creates an array out of nonArrayObject
   ``` const arrayFromNonArray = Array.from( nonArrayVector, optionalFunctionToProccessEachElement) ```
   - Array.of() - creates a an array of arguments passed as params 
        ``` const array = Array.of(1,3,4,56); ```
   - find() - searches for a element in array 
        ``` const found = searchIn.find(post => post.code === 1) ```
   - findIndex() - searches for the index of a specific element 
        ``` const found = searchIn.findIndex(post => post.code === 1) ```
   - some() - check if some of the array elements meet a requirement 
            - returns boolean
        ``` array.some(element => element.age > 20); ```
   - every() - check if every array elements meet a requirement 
            - returns boolean
        ``` array.every(element => element.age > 20); ```
   
### Object defining
``` 
    const tshirt = { 
        [key]: value, 
        [`${key}Opposite`]: invertColor(value), 
        [keys[0]]: value,
    }
```
   
### Exports
- default export => variables can be inported with any name 
    - {} **NOT** needed
- named export => variables can be imported only with the original name
        - {} needed
        - variables can be renamed in the file where imported with ```as``` keyword
        


### Generator function
- function that can be started or stopped 
- can also be looped through with ```for...of ```
- contains yield, that sets the "breakpoints" 
- to pass each breakpoint, you have to store the generator function inside a variable 
        ``` const people = listPeople(); ```
- and then call next on that variable
        ```people.next() //will return the first yield as a an object { yieldValue, done:true/false }``` 

  **example:**
``` 
    function* loop(array) {
        for(const item of array) {
            yield item; //will return a item on next() call
            }
    }
 ```
   ***example with ajax calls***
``` 
    function ajax(url) { 
        fetch(url).then(data => data.json()).then(data => dataGenerator(data)); //      3.    this will fetch and when data is received, this will restart the chain for the url2
    }

    function* steps(array) {
        const call1 = yield ajax(url1);   //      2.    this will call the ajax function, that will fetch 
        const call2 = yield ajax(url2);
        const call3 = yield ajax(url3);
    }

    const dataGenerator = steps; 
    dataGenerator.next(); //      1.     this will trigger the fetch chain
```
   
   ### Proxies
   - allows overriding an object property 
``` 
    const objectToBeProxied = { name: 'Denisa', age: 22 }; 
    // const proxy = new Proxy( target, handler );
    const proxy = new Proxy( objectToBeProxied, { 
        get(objectToBeProxied, name) {
            return objectToBeProxied[name].toUpperCase(); 
        }
        set(objectToBeProxied, name, value) {
            objectToBeProxied[name] = value.trim(); 
        }
    });
    proxy.name = 'Andreea'; 
```
### Sets & weak Sets
- sets are a kind of unique items array
- main properties of sets: ```size```, ```delete('denisa')```, ```clear()```, ```entries()```, ```keys()```, ```has()```, ```add()```
- ```values()``` will return a iterator, that can be looped through with ```for..of``` or ```.next()```
- calling ```next()``` on iterator will remove returned items from the iterator
- ***Weak Sets*** are almost the same with sets
    - they can only contain objects 
    - cannot be looped through with for..of because they can't generate an iterator
    - they don't have a ```clear()``` method, because they clean themselves up by garbage colector, everytime a reference of the object is deleted

### Maps and weak Maps
- maps are similar to ***sets***, but they have a key and a value
- can have an object as a key
- can be used as metadata dictionary
    - for example, a map with a bunch of buttons as keys and the number of clicks per each button as value
- methods: ```has(key)```, ```get(key)```, ```delete(key)```
- can be looped through with ```.foreach()``` and ```for..of```

- ***weak map*** doesn't  have a size, is not enumerable and garbage collected as the sets
- normal map will still hold the deleted element and this will create a memory leak.
