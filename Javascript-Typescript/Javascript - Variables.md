Voir plus du ESM que du CJS

## Variables
The **var** ("old school") keyword , declares a function-scoped or globally-scoped variable.
```javascript
var x = 1;

if (x === 1) {
  var x = 2;
  console.log(x);
  // Expected output: 2
}
console.log(x);
// Expected output: 2
```

The **let** keyword, declares re-assignable, block-scoped local variables.
```javascript
let x = 1;

if (x === 1) {
  let x = 2;
  console.log(x);
  // Expected output: 2
}
console.log(x);
// Expected output: 1
```
Naming the same variable in the same scope trigger an error.

The **const**  keyword, declares block-scoped local variables it can't be changed using an assignment operator, but if a constant is an **object** it's properties can be added, updated or removed.
```javascript
const number = 42;

try {
  number = 99;
} catch (err) {
  console.log(err);
  // Expected output: TypeError: invalid assignment to const 'number'
  // (Note: the exact output may be browser-dependent)
}
console.log(number);
// Expected output: 42
```

## Hoisting


## Scopes
In addition to the traditional Global scope, Function scope and Block scope, JavaScript have the **modules scopes.** 
The latter provide a way to encapsulate variables within a module, preventing them from polluting the global scope.

# Source

[[Javascript-Typescript Source]]
