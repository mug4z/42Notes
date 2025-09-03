cdTO SEARCH:
- What the fuck is INLINE 
This: Represente un pointeur vers l'instance courante .
## Classes
Defined in a hpp file.
- Is a template that define the form of an object.
- create a new data type that can be used to create objects.
- Define both code and data.
- Essentially a set of plans that specify how to build an object.
- A class is a logical abstraction.
- A class exist in memory when an object of that class have been created.
- The code and data that constitute a class are called **members** of the class.
- Private members can only be accessed  by other members of their class and not by any other part of the programm.
	- By default all members are private.
- A class must have only one logical entity.
- Protected
	- ``

Simple Exemple (data only class):
```c++
class Vehicle
{
	public:
		int passengers;
		int fuelcap;
		int mpg;
};
```
	
- When you add a function to a class it's not need to be prototyped elsewhere.
Simple Exemple (With function)
```c++
class Vehicle
{
	public:
		int passengers;
		int fuelcap;
		int mpg;

		int range(); // Function member
};
```

- In a ClassCode.cpp we can implement the function.
- The **::** (scope operator) links a class name with a member name in order to tell the compiler what class the member belongs to.
- When a member function uses an instance variable tha is defined by its class it does so directly.
```c++
int Vehicle::range()
{
	return (mpg * fuelcap)
}
```
## Constructor and Destructor
Constructor have no explicit return type, same thing for destructor.
- Constructor: Define what actions occurs when the object is initialized.
- Destructor: Define what actions occurs when the object is destroyed (aka: We go out of it's scope)
Exemple
```c++
class_name(); // Constructor
~class_name(); // Destructor
```

### Orthodox Canonical Form
```c++
class Vehicle
{
	public:
		Vehicle(); // Constructor
		Vehicle(const Vehicle &a); // Copy constructor
		~Vehicle(); // Desctructor
		Vehicle & operator = (const Vehicle &a);
}
```

#### Copy constructor
A copy constructor is used to initialize an object based with the same object 

```c++
Fixed::Fixed(const Fixed &other)
{
	this->_fixed = other._fixed;
	std::cout << "Copy constructor called" << std::endl;
}
```

#### Copy assignment operator
```c++

```

### Objects
- Objects are instances of a class
- Object are seperated with each other.
Exemple of an object
```c++
Vehicle minivan; // minivan is an instance of Vehicle class thus an object.
minivan.mpg; // Access the members of object minivan using . (dot) operator.
```
## Static function member

There are not associated with any object. When called they have not *this* pointer.
So it can be used  without the need to instanciate an object.

## Static data member
A static data member will share it's value amongst the different instance of the class.
Static data member need to be initialize outside of the class usually in the cpp file.
```c++
// In cpp
int Class::static_member = 0;
// Rest of cpp

```
## Inheritance
The base class is constructed first

### Public inheritance
makes `public` members of the base class `public` in the derived class, and the `protected` members of the base class remain `protected` in the derived class.

### Private inheritance
makes the `public` and `protected` members of the base class `private` in the derived class.

### Protected inheritance
makes the `public` and `protected` members of the base class `protected` in the derived class

##  Polymorphism
Doing different things with the same name. Like function overloading.
Example:
```c++
void print(int num) {
	std::cout << "Printing int: " << num << std::endl;
}

void print(double num) {
	std::cout << "Printing double: " << num << std::endl;
}
```

### Compile-time polymorphism

```c++
void print(int num) {
	std::cout << "Printing int: " << num << std::endl;
}

void print(double num) {
	std::cout << "Printing double: " << num << std::endl;
}
```

#### Template
Template is a way to create generic function or classes. The actual code for specific types is generated at compile time.
```c++
#include <iostream>

// Template function to print any type
template<typename T>
void print(const T& value) {
    std::cout << "Printing value: " << value << std::endl;
}

int main() {
    print(42);           // int
    print(3.14159);      // double
    print("Hello");      // const char*

    return 0;
}
```

### Runtime Polymorphism
Also named dynamic polymorphism, it a technique where a derived class can override or redefine method of it's base class.
- These methods (in base classs) needs to be created with the virtual keyword.
- In Derived class use the override keyword (only in c++11)
- In cpp 98 remove the override keyword.
- ATTENTION: if you removed the virtual keyword when accessing by reference the draw method it will be the base draw used instead of the derived one.
- ATTENTION if one of the method is virtual thus the destructor needs to be virtual as well.

```c++
#include <iostream>

// Base class
class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape" << std::endl; 
    }
};

// Derived class 1
class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle" << std::endl; 
    }
};

// Derived class 2
class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a rectangle" << std::endl;
    }
};

int main() {
    Shape* shape;
    Circle circle;
    Rectangle rectangle;

    // Storing the address of circle
    shape = &circle;

    // Call circle draw function
    shape->draw();

    // Storing the address of rectangle
    shape = &rectangle;

    // Call rectangle draw function
    shape->draw();

    return 0;
}
```

#### Virtual Method
Virtual functions are member functions whose behavior can be overridden in derived classes.
If a derived class is handled using pointer or reference to the base class, a call to an overridden virtual function would invoke the behavior defined in the derived class.

If in a derived class there is a member function with the same:
- Name
- parameter type list (but not the return type)
- cv-qualifiers
- ref-qualifiers
of it's base class and in the base class the member function is declared as virtual. Thus the derived member function is also virutal even if  there is no virtual keyword.
##### Virtual destructor
Even though destructors are not inherited, if a base class declares its destructor `virtual`, the derived destructor always overrides it. This makes it possible to delete dynamically allocated objects of polymorphic type through pointers to base.

###  Abstract Class
An abstract class is a class which contain at least one pure virtual function member. And don't specify the implementation of such function. Also they can't be initialized.
```c++
// An abstract class
class Test {
    // Data members of class
public:
    // Pure Virtual Function
    virtual void show() = 0;

    /* Other members */
};
```

ATTENTION: If you don't specify the implementation for the virtual member function the derived class will be also abstract.
#### Deep Copy 
A deep  copy of an abstact class. Is somehow tricky.
#### Interfaces
Pure abstract class are called interfaces.

- [x] Classes
- [x] Orthodox Canonical Form
	- [x] Constructor
	- [x] Destructor
	- [x] Copy constructor
	- [x] Copy assignment operator
- [x] Objects
- [x] methods
- [ ] Encapsulation
- [x] Inheritance
- [ ] Polymorphism
- [x] Abstraction
- [ ] Namespace

# Source
[[CPP - Source]]
