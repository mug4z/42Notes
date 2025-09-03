
## Static
Done at compile time

## Dynamic.
Done at run time and work for 
```c++
dynamic_cast<target-type>(exprr)
```

Otherwise, the runtime check fails.

- If target-type is a pointer type, the result is the null pointer value of target-type.
- If target-type is a reference type, an exception of a type that would match a [handler](https://en.cppreference.com/w/cpp/language/catch "cpp/language/catch") of type [std::bad_cast](https://en.cppreference.com/w/cpp/types/bad_cast "cpp/types/bad cast") is thrown.

## Reinterpret cast
- It is used to convert a pointer of some data type into a pointer of another data type, even if the data types before and after conversion are different.
- It does not check if the pointer type and data pointed by the pointer is same or not.
# Source
[[CPP - Source]]