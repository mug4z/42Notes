
check the
	std::ios init(NULL);
	init.copyfmt(std::cout);
	std::cout.copyfmt(init);
	std::istringstream
### std::istringstream
Allow you to perform input operations on strings.

### copyfmt

```c++
copyfmt(const basic_ios& other);
```
If other refers to the same object as *this, has no effects. 
Otherwise, copies the state of the stream other into *this*.
### EOF
Stand for end of file.

### Find
returns the posistion of the beginig ocurence.
# Source
[[CPP - Source]]

