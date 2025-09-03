## References
created with the & operator.
```c++
string food = "Pizza";  
string &meal = food;
```
in the above exemple meal is a reference to food.
A reference CANNOT be null and must be constant.
It's like a pointer not null and constant. 
If you changed the reference meal, the value of food will be replaced as the reference have a single memory location.

## Pointers

### Pointers to function members
Pointers to members allow you to refer to nonstatic members of class objects
Declare and setting a pointer to member function 
```c++
// Assume that X is a class and f a function member.
  void (X::* ptfptr) (int) = &X::f;
```
Using a pointer to member function
```c++
(this->*ptfptr)(39);
```

# Soure
[[CPP - Source]]