## Callback
Function that is passed into another function.
### Callback hell
Call callbacks inside callbacks.
Promises solve this problems .

## Promises
Object returned by an asynchronous function.
**fetch()** is the modern replacements for XMLHttpRequest.
A promise can be in one of three states:
- **pending**: Initial state. The operation has not yet completed.(Success of failed)
- **fulfilled**: The operation succeeded. This when the promise's `.then()` handler is called
- **rejected**: The operation failed. This is when the promise's `.catch()` handler is called.
### Promise chaining
```javascript
const fetchPromise = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
  .then((response) => response.json())
  .then((data) => {
    console.log(data[0].name);
  });
```

### Error handling
```javascript
const fetchPromise = fetch(
  "bad-scheme://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log(data[0].name);
  })
  .catch((error) => {
    console.error(`Could not get products: ${error}`);
  });
```



## Async/await



# Source
[[Javascript-Typescript Source]]