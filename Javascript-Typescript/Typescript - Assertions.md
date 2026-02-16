[[Typescript - Data Types]]

## Type Assertions

Sometimes you will have information about the type of a value that TypeScript can’t know about.

For example, if you’re using `document.getElementById`, TypeScript only knows that this will return _some_ kind of `HTMLElement`, but you might know that your page will always have an `HTMLCanvasElement` with a given ID.

In this situation, you can use a _type assertion_ to specify a more specific type:
```typescript
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```

> [!warning] 
> Like a type annotation, type assertions are removed by the compiler and won’t affect the runtime behavior of your code.
> Also this is mentioned as unsafe in the  [google style guide](https://google.github.io/styleguide/tsguide.html#type-and-non-nullability-assertions)
## const assertions

```typescript
// Type '"hello"'  
let x = "hello" as const;  
// Type 'readonly [10, 20]'  
let y = [10, 20] as const;  
// Type '{ readonly text: "hello" }'  
let z = { text: "hello" } as const;
```

## Non Null Assertion 

The non-null assertion operator is used to assert that a value is not null or undefined, and to tell the compiler to treat the value as non-nullable. However, it's important to be careful when using the non-null assertion operator, as it can lead to runtime errors if the value is actually `null` or `undefined`.
```typescript
let name: string | null = null;

// we use the non-null assertion operator to tell the compiler that name will never be null
let nameLength = name!.length;
```
> [!warning] 
> Also this is mentioned as unsafe in the  [google style guide](https://google.github.io/styleguide/tsguide.html#type-and-non-nullability-assertions)

## Satisfies 
The `satisfies` operator lets us validate that the type of an expression matches some type, without changing the resulting type of that expression.

It can be useful for typescript to tell you if you make mistake with the type you set yup.
```typescript
type Colors = "red" | "green" | "blue";
// Ensure that we have exactly the keys from 'Colors'.
const favoriteColors = {
    "red": "yes",
    "green": false,
    "blue": "kinda",
    "platypus": false
//  ~~~~~~~~~~ error - "platypus" was never listed in 'Colors'.
} satisfies Record<Colors, unknown>;
// All the information about the 'red', 'green', and 'blue' properties are retained.
const g: boolean = favoriteColors.green;
```
# Source
[[Javascript-Typescript Source]]

#Typescript #Assertions
