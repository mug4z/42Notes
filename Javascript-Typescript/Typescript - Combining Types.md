## Combining Types
## Union Types
You can combine types with the union operator `|`. Using the `type` keyword in order to create an alias  (like with typedef).
In the example below the stringOrNumber is a `string` or a `number`.
```typescript
type stringOrNumber = string | number;
let value: stringOrNumber = 'hello';

value = 42;
```

> [!warning] 
> Typescript will only allow an operation if it is valid for every member of the union.
> ```Typescript
> function printId(id: number | string) {  
> 	console.log(id.toUpperCase());
> // Property 'toUpperCase' does not exist on type 'string | number'.
   // Property 'toUpperCase' does not exist on type 'number'.
> }
> ``` 

It exist a way to bypass this limitation by *narrow* union with code. 
TODO: link to the narrow concept.
```typescript
function printId(id: number | string) {  
	if (typeof id === "string") {    
	// In this branch, id is of type 'string'    
	console.log(id.toUpperCase());  
	} else {    
	// Here, id is of type 'number'    
	console.log(id);  
	}
}
```
## Type Intersection



# Source
[[Javascript-Typescript Source]]

#Typescript #CombiningTypes #DataType 