## Types of storage
### Local storage
- simple key-value store
- manage user preferances or basic user data
- can be cleared by user/JS
```characteristics:``` 
- easy to use
- versatile 
- bad for complex data

##### Usage:
- synchronous code
- ``` window.localStorage ``` accessing local storage
- ```localStorage.setItem(key, value)``` add element to storage
    - will call ```toString()``` when storing data, so primitive data will be stored as usual, but objects will be stored as [Object object]
    - to store ***objects***: ```JSON.stringify(object)```
- ``` localStorage.getItem(key)``` get element from storage
    - to read ***objects***: ```JSON.parse(localStorage.getItem('object'));```
- ``` localStorage.removeItem('myCat'); ```
- ``` localStorage.clear(); ```

#### Local vs. Session Storage: 
```Local storage```
- data is available even after reopening the browser

```Session Storage ```
- data is available as long as the browser is open
- available after refresh

### Cookies
- simple key-value store 
- can be added extra configs
- manage user preferances or basic user data
- can be cleared by user/JS
```characteristics:``` 
- clunky to use
- versatile
- sent to server 
- bad for complex data

#### Usage:
- need a server to read them 
- ``` document.cookie = `key= ${value}` ```
- store objects using ```key= ${JSON.stringify()}```
- retrieve objects using ```document.cookie.split(';')```, because data is stored as String
- setting expiration date, using max-age or expires ```document.cookie = `key= ${value}; max-age=2` || expires='date-format'```

#### Adavantage: 
- can be set to expire
- can be sent to server as request

### IndexedDB
- sophisticated, client-side datebase
- manage complex data 
- can be cleared by user/JS
```characteristics:``` 
- clunky
- great for complex data
- good performance

#### Usage: 
- establish database ```indexedDB.open('uniqueNameGivenByUser', versionOfDB)```
```
dbRequest.onsuccess = function(event) {
    const db = event.target.result;
    const obj = db.createObjectStore('products', {keyPath: 'id'});
    obj.transaction.oncomplete = function(event) {
        const productsStore = db
            .transaction('products', 'read/write/readwrite')
            .objectStore('products');
        
        productsStore.add({
            id:'p1', 
            title:"Prod", 
            price: 12.2, 
            tags:["cheap", "hipster"]
        });
    }
}
 dbRequest.onerror = function(event) {}
 ```
 - retrieve from DB
 ```
 const productsStore = db
            .transaction('products', 'read/write/readwrite')
            .objectStore('products');
const request = productsStore.get('p1');
request.onsuccess = function() {
    //actions
}
 ```
 

