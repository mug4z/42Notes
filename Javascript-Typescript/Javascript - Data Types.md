- [ ] Avoir fait le tour de la base de javascript 📅 2025-05-12

## Primitive
### Number
Represent both integer and floating point numbers, up to **+-2^53**
```javascript
let num = 42;
let num2 = 255.0;      // floating-point number with no fractional part
let num3 = 0xff;       // hexadecimal notation
let num4 = 0b11111111; // binary notation
let num5 = 0.255e3;    // exponential notation
```

It also have the **Infinity** and **-Infinity** in case division by 0.
```javascript
alert(1 / 0 ); // Infinity
```

**NaN** represent a computational error.
```javascript
alert("not a number" / 2); // NaN
```

### BigInt

> [!warning] 
> BigInt value **cannot** be used with methods in the built-in **Math object** and cannot be mixed with a Number value in operations; they must be coerced to the same types.

BigInt is a built-in JavaScript object that allows you to work with integers of arbitrary size (biger that number can handle).
```javascript
const previouslyMaxSafeInteger = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991);
// 9007199254740991n

const hugeString = BigInt("9007199254740991");
// 9007199254740991n

const hugeHex = BigInt("0x1fffffffffffff");
// 9007199254740991n

const hugeOctal = BigInt("0o377777777777777777");
// 9007199254740991n

const hugeBin = BigInt(
  "0b11111111111111111111111111111111111111111111111111111",
);
// 9007199254740991n
```

## String

> [!information]   
> There is no character type. Only string wito zero, one and many characters.

Must surrounded by quotes.
```javascript
const string1 = "A string primitive";
const string2 = 'Also a string primitive';
const string3 = `Yet another string primitive`;
```

Backticks quote are extended functionality quotes, they allow to embed variables and expressions into a string.
```javascript
let phrase = `can embed another ${string1}`;
```
## Boolean
Represent true or false.
```javascript
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked
```

## Null
Means **nothing, empty or value unknown** it is not a reference to a non-existing object or Null pointer.
```javascript
let age = null;
```

## Undefined
Unintialized data.
```javascript
let age;

alert(age); // shows "undefined"
```

# Source
[[Javascript-Typescript Source]]

#Javascript #DataType 