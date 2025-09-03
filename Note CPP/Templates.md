## Function templates
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


## Template array
It's the same way as function template.

```c++
template<typename T>
void iter(T &array, int size, void (*f)(T &ar, int index))
{
	for(int i =0 ; i < size; i++)
	{
		f(array,i);
	}
}
```

## Class Template
It's how you declare class template. You need to specify the type when you create the object.

```cpp
template<typename T>
class Array{
	private:
		T *_array;
	public:
		Array(void)
		{
			T _array = new T [0];
		}
		~Array();
		Array(const Array &other);
		Array & operator= (const Array &other);

};
// in main
int main()
{
	Array<int>test();
}
```

## Dependent names
A dependent name is a name that depends on a template parameter.

The T::iterator is dependent on T because it is not known until the point of instantiation.
Is there to use the iterator of the T types.

typename states that the name that follows should be treated as a type.
```cpp
template<typename T>
typename T::iterator easyfind(T &array, int i_toFind)
{
	typename T::iterator it = std::find(array.begin(),array.end(),i_toFind);
	if(it != array.end())
		return (it);
	else
		throw (std::runtime_error("No occurence found"));
}
```