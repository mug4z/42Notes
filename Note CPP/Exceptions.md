An exception is an object, with a what member. The what member contain the message to print when the error is throwed. It helps indicating what went wrong.

If in a function in a try statement catch an error the last try catch is ignored.
## Attention
- If you throw an exception but you don't catch it the programm will crash.
- Make sure the catch is the same type of the throw.
## try  catch throw
### try
Test the code that could throw an error.
### throw
Throw an exception to be catch.
```c++
//throw expressions
throw(123);
throw(Object);
```
### catch
catch the error throwed, the type throwed must be the same in the catch keyword.

### Exemple
The following example show that throw can be used inside a function to be catch in the calling function.
```c++
void testExceptions();
int main()
{
	try
	{
		testExceptions();
	}
	catch(int i)
	{
		std::cout << "i have " << i << " value" <<  std::endl;
	}
	return (1);
}

void testExceptions()
{
	int i = 10;
	if(i == 9)
	{
		std::cout << "i is good" << std::endl;
	}
	else
		throw (i);
}
```
Output: i have 10 value;

## Exception Class (Custom exception)
An exception Class is derived from the std::exception base class.
Thus we have to implement the what member.
All class derived from std::exception can be catch using an reference of exception (std::exception &e)

A little example of an exception class (Custom exception). 
```c++
// IN HPP file
class GradeTooHighException : public std::exception
	{
		public:
			virtual const char * what() const throw();
	};
// IN CPP file
const char *GradeTooLowException::what() const throw()
{
	return ("MESSAGE")
}

// IN MAIN
#include "GradeTooHigh.hpp"
int main()
{
	try
	{
		if (grade <= MAX_VALUE)
			throw (GradeTooHighException());
	}
	catch(std::exception &e)
	{
		std::cout << e.what << std::endl;
	}

}
```

# Source
[[CPP - Source]]