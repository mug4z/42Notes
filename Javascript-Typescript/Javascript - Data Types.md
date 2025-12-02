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
BigInt is a built-in JavaScript object that allows you to work with integers of arbitrary size.


# Source
[[Javascript-Typescript Source]]

#Javascript #DataType 