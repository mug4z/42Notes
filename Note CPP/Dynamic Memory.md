## new

```c++
void* operator new(std::size_t);
```
if it fails throws bad_alloc exeptions.

### Allocating an int
```c++
int *p
try
{
	p = new int;
}
catch(bad_alloc xa)
{
	std::cout << "Allocation Failure" << std::endl;
}
```
### Allocating an array
```c++
int *p

try
{
	p = new int [10]
}
catch (bad_alloc xa)
{
	std::cout << "Allocation failure" << std::endl;
}
```

### Allocating an object
When dynamically creating an object you will trigger the constructor of this object.
```c++
Class_name *object;
try{
	object = new Class_name; // Here the constructor is triggered
}
catch (bad_alloc xa)
{
	std::cout << "Allocation failure" << std::endl;
}
```
## delete
```c++
delete allocated_var;
```
### Delete an allocated int

```c++
delete p;
```
### Delete an allocated array
```c++
delete [] p;
```
### Delete an allocated object
```c++
delete object; // Calls the destructor of the object.
```

# Source
[[CPP - Source]]