### JS Types
***I. Primitives***
= immutables = cannot be modified because this means to change what's in memory, which is not allowed
= passed by value => it is asigned only the value, not the reference of primitive in memory
1. Number
2. Boolean
3. String
4. Undefined
    - missing of deffinition
5. Symbol
    ```Symbol('')```

***II. Non-primitives***
= passed by reference
6. Object
    - ***null*** = missing of value
    - {}
        - ```obj2 = Object.assign({}, obj1)``` will create a new object with same properties and values as obj1, but at different address in memory
        - ```obj3 = {...obj1} ```
    - [] - arrays
        - ```arr2 = [].concat(arr1)``` will create a new array with same values of array1, but at different address

```Object.is()``` works the same as ```===``` but more accurate for cases like ```-0 and +0```, ```NaN and NaN```

***Deep cloning*** 
```let superClone = JSON.parse(JSON.stringify(obj))```

***Type coercion***
- ```==``` will convert a type to another type and then compare the values
    - ```5 == '5'``` will be true
- ```===``` compare the values without converting
    - ```5 === '5'``` will be false

- happens in if statement, too

### Dynamic vs Static Languages
- ***Dynamic***: 
    - don't need to specify the kind of variable
    - variable type is set at runtime
- ***Static***: needs the kind of variable


