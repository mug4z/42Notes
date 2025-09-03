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
		Vehicle(const Vehicle &a);
		~Vehicle(); // Desctructor
		Vehicle & operator = (const Vehicle &a);
}
```
### Objects
- Objects are instances of a class
- Object are seperated with each other.
Exemple of an object
```c++
Vehicle minivan; // minivan is an instance of Vehicle class thus an object.
minivan.mpg; // Access the members of object minivan using . (dot) operator.
```
## Interface
- Default constructor
- Copy constructor
- Destructor
- Copy assignment operator

### Theory to cover

- [ ] Classes
- [ ] Orthodox Canonical Form
- [x] Objects
- [x] methods
- [ ] Encapsulation
- [ ] Inheritance
- [ ] Polymorphism
- [ ] Abstraction
- [ ] Namespace

# Source
[[CPP - Source]]
