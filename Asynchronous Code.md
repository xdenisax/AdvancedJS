## Promises 
***Def:*** A promise is an object that may produce a single value some time in the future and has 3 possible states: 
1. **fulfilled:** ```resolve()``` will be called
2. **rejected:** ```reject()``` will be called
3. **pending:** object is neither fulfilled, nor rejected.

***Settled*** == **resolved / rejected**

```!!!``` Once settled, a promise cannot be resettled ```=>``` calling resolve()/reject() won't have any effect ```=>``` promises are immutable

***Chaining promises***
- with ```then```
- allows multiple ```then```s in a row, with the condition that the previous promise returns

***Native functions***
- ```Promise.reject()``` returns a rejected promise.
- ```Promise.resolve()``` returns a resolved promise.
- ```Promise.race()``` ***takes an array*** (or any iterable) and ***returns a promise*** that resolves with the value of the ***first resolved*** promise in the iterable, ***or*** rejects with the reason of the ***first*** promise that ***rejects***.
- ```Promise.all()``` ***takes an array*** (or any iterable) and ***returns a promise*** that ***resolves when all*** of the promises in the iterable argument have ***resolved***, ***or rejects*** with the ***reason of the first*** passed promise that ***rejects***.
- ```Promise.allSettled()``` ***takes an array*** (or any iterable) and ***returns an array*** with all the promises ***resolved*** or ***rejected***.


