
## Type Inference
It just means that typescript can automatically determine the type of a variable based on the value assigned to it
```Typescript
let name = "Ouioui";
```
## Type Compatibility
Two types are considered compatible if they have the same structure, regardless of their names.
```typescript
interface Point {
  x: number;
  y: number;
}

let p1: Point = { x: 10, y: 20 };
let p2: { x: number; y: number } = p1;

console.log(p2.x); // Output: 10
```
`p1` and `p2` are not of the same type, but they are compatible because they have the same structure.
## JavaScript types
[[Javascript - Data Types]]

## Primitive
### Void
Represents the return value of function which don't return a value.
```typescript
// The inferred return type is void
function noop() {
  return;
}
```

## Object Types
### Interface
Type an object using an interface that can be reused by multiple objects.
```typescript
interface Person {  
	name: string;  
	age: number;
} 
function greet(person: Person) {  
	return "Hello " + person.name;
}
```

### Class
Like in c++ we have classes.
```typescript
class Car {
  make: string;
  model: string;
  year: number;

  constructor(make: string, model: string, year: number) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  drive() {
    console.log(`Driving my ${this.year} ${this.make} ${this.model}`);
  }
}
```
### Enum
Woks like in C++ or C
```typescript
enum Direction {
  Up = 1,
  Down, // 2
  Left, // 3
  Right, // 4
}
```


### Array
In this example I made an number array with `number[]`, this syntax works for **any type** . (`string[]`)
```typescript
const numbers: number[] = [1, 2, 3];
```

### Tuple
A tuple type is another sort of Array type that knows exactly how many elements it contains, and exactly which types it contains at specific positions.
```typescript
type StringNumberPair = [string, number];

const pair: StringNumberPair = ['hello', 42];

const first = pair[0];
const second = pair[1];

// Error: Index out of bounds
const third = pair[2];
```

### Object
To define object we simply list its properties and their types. This function take a point-like object.
```typescript
// The parameter's type annotation is an object type
function printCoord(pt: { x: number; y: number }) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}

printCoord({ x: 3, y: 7 });
```

## Top types
### Any
TypeScript has a special type, `any`, that you can use whenever you don’t want a particular value to cause typechecking errors.

When a value is of type `any`, you can access any properties of it (which will in turn be of type `any`), call it like a function, assign it to (or from) a value of any type, or pretty much anything else that’s syntactically legal:

```typescript
let obj: any = { x: 0 };
// None of the following lines of code will throw compiler errors.
// Using `any` disables all further type checking, and it is assumed
// you know the environment better than TypeScript.
obj.foo();
obj();
obj.bar = 100;
obj = 'hello';
const n: number = obj;
```

### Unknown
`unknown` is the type-safe counterpart of `any`. Anything is assignable to `unknown`, but `unknown` isn’t assignable to anything but itself and `any` without a type assertion or a control flow based narrowing. Likewise, no operations are permitted on an `unknown` without first asserting or narrowing to a more specific type.
```typescript
function f1(a: any) {
  a.b(); // OK
}

function f2(a: unknown) {
  // Error: Property 'b' does not exist on type 'unknown'.
  a.b();
}
```


## Bottom types
### Never
TODO check that in details if needed.
```typescript
// Function returning never must not have a reachable end point
function error(message: string): never {
  throw new Error(message);
}

// Inferred return type is never
function fail() {
  return error('Something failed');
}

// Function returning never must not have a reachable end point
function infiniteLoop(): never {
  while (true) {}
}
```

Also we have 
[[Typescript - Assertions]]


# Source
[[Javascript-Typescript Source]]

#Typescript #DataType 
