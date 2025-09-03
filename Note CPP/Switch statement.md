
### Explicit fallthrough
```c++
	switch (levels)
	{
		case 0:
			(this->*function[0])();
			__attribute__((fallthrough));
		case 1:
			(this->*function[1])();
			__attribute__((fallthrough));
		case 2:
			(this->*function[2])();
			__attribute__((fallthrough));
		case 3:
			(this->*function[3])();
			break;
		default:
			std::cout << "[ Probably complaining about insignificant problems ]" << std::endl;
	}

```

# Source
[[CPP - Source]]