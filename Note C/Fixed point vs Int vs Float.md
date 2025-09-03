## Float
Float point representations can vary from machine to machine.
But the standard IEEE-754 is here to save you.

IEEE-754 float is 4 bytes and double is 8 bytes
There are 3 components:
- a sign bit (telling if the number is + or -) : 1 bit
- Exponent (its order of magnitude) : 8 bits
- mantissa (actual digits of the number) : 23 bits

```
seeeeeeeemmmmmmmmmmmmmmmmmmmmmmm

s = sign bit, e = exponent, m = mantissa
```

The value of the number is the mantissa times 2^x
(x = the exponent)

In general: number = (sign ? -1:1) * 2^(exponent) * 1.(mantissa bits).


## Fixed point number.
Fixed Point Representation means real numbers (numbers with fractional part) where the position of the decimal point is fixed.
Number split into an integer part and an fractional part.

## Shifting pattern
When an integer right shifted by 1 bit. It's like dividing the number by 2.
Exemple
```
00000010 = 2
Shift the bit to the right, so dividing 2 by 2.
00000001 = 1
```

The other way around is also possible,it will multiplied the number by 2
```
00000001 = 1
Shift the bit to the left, so multiplying 1 by 2.
00000010 = 2
```

## Representation of Binary point
Binary point is like the decimal point in base 10 system.

Everything to the left of binary point will be 2^1 2^2 ..

```
The point is equal to 2^0
11010.1
All bits to the left are represented like 2^1 2^2 ..
All bits to the right are represented like 2^-1 2^-2
```

