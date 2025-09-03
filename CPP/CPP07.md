# Ex01
- [x]  Function iter
	- [x] Address of an array
	- [x] lenght of the array
	- [x] Function that will be called on each element of the array
# Ex02

https://stackoverflow.com/questions/5513545/template-memory-allocation
- [x] Constructor with no parameter: Create an empty array.
- [x] Construction with an unsigned int n as a parameter
- [x]  Elements can be accessed through the subscript operator: [ ].
- [x] When accessing an element with the [ ] operator, if its index is out of bounds, an std::exception is thrown
- [x]  A member function size() that returns the number of elements in the array. This member function takes no parameter and musn’t modify the current instance
- [x] Construction by copy and assignment operator. In both cases, modifying either the original array or its copy after copying musn’t affect the other array.
- [x] You MUST use the operator new[] to allocate memory. Preventive allocation (allocating memory in advance) is forbidden. Your program must never access nonallocated memory.
- [ ] A Faire:
	- [ ] Plusieur test pour verifier le bon fonctionement du templates, surtout le faire a tete reposer.
	- [ ]