The variable are immutable by default.

It means that they can't change.
```rust
fn main() {
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```
This code wont compile.
In order to change a variable, you have to specify it as mutable with the keyword `mut`
```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

This  declare a constant.
```rust
const HELLO = 42;
```

# Source

[[Rust - Source]]