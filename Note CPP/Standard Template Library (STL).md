- [ ] Voir plus en details:
	- [x] les vector
	- [x] les list
	- [x]  les deque
	- [ ] les Associative containers
		- [ ] set
			- [ ] red black trees
		- [ ] map
	- [ ] Les iterators

## Containers
It give the programmer a set of tools to easily implement common data structure like queues, list and stacks.

The container manages the storage space that is allocated for its elements and provides member functions to access them, either directly or through iterators (objects with properties similar to pointers).

### Sequence Containers
These are linear data structures that store elements in a sequential manner.
#### Vector
A dynamic array that grows and shrinks at runtime.
```cpp
std::vector<int> my_vector;
w```
The elements are stored contiguously. Which means that elements can be accessed not only through iterators, but also using offsets to regular pointers to elements

Vector usually occupy more space than static arrays. Because more memory is allocated to handle future growth. It only expand when the additional memory is exhausted.
When the memory expand the vector need to find more space allocated the memory and copy the data into the new memory place.

Add data in vector with push_back
```cpp
std::vector<int> my_vector2;
my_vector2.push_back(23);
std::cout << "Vector2 capacity in elements: " << my_vector2.capacity() << std::endl;
```
Add data in vector using constructor, the exemple below create a vector of 10 elements which value is 100.
```cpp
std::vector<int> my_vector (10,100);
```
##### Capacity
The total amount of allocated memory can be queried using `capacity()`
```cpp
std::vector<int> my_vector (10,100); // create a vector of 10 elements which value is 100
my_vector.push_back(42);
std::cout << "Vector capacity: " << my_vector.capacity() << std::endl; // return 20
```
It returns the number of elements that the container has currently allocated space for.

You can reserve so it eliminate the reallocation if the number of elements is known beforehand. 
It increase the capacity of the vector can hold without requiring reallocation.
```cpp
vector<int> my_vector;
my_vector.reserve(SIZE); // Allocate SIZE * sizeof(int)*
```

shrink_to_fit() are in more recent version of c++.

##### Complexity
The complexity (efficiency) of common operations on vectors is as follows:
- Random access - constant 𝓞(1).
- Insertion or removal of elements at the end - amortized constant 𝓞(1).
- Insertion or removal of elements - linear in the distance to the end of the vector 𝓞(n).

#### List
A doubly linked list
```cpp
std::list<int> my_list;
```
`std::list` is a container that supports constant time insertion and removal of elements from anywhere in the container. Fast random access is not supported.

Adding, removing and moving the elements within the list or across several lists does not invalidate the iterators or references.

Some example of list usage.
```cpp
std::list<int> my_list(10,100);
std::list<int>::iterator it;
std::cout << "First element of my list :" << my_list.front() << std::endl;
std::cout << "Last element of my list :" << my_list.back() << std::endl;
std::cout << "List capacity in elements:" << my_list.size() << std::endl;
std::cout << "List maximum capacity in elements:" << my_list.max_size() << std::endl;
std::cout << "Iterate through the list" << std::endl;
for(it = my_list.begin() ; it != my_list.end() ; ++it)
	std::cout << (*it) << std::endl;
std::cout << "List pop first element" << std::endl;
my_list.pop_front();
std::cout << "List capacity in elements:" << my_list.size() << std::endl;
```
#### Deque
A double-ended queue allowing insertion and deletetion on both ends.
```cpp
std::deque<int> my_deque;
```
`std::deque` (double-ended queue) is an indexed sequence container that allows fast insertion and deletion at both its beginning and its end. In addition, insertion and deletion at either end of a deque never invalidates pointers or references to the rest of the elements.

As opposed to [std::vector](https://en.cppreference.com/w/cpp/container/vector "cpp/container/vector"), **the elements of a deque are not stored contiguously**: typical implementations use a sequence of individually allocated fixed-size arrays, with additional bookkeeping, which means indexed access to deque must perform two pointer dereferences, compared to vector's indexed access which performs only one.

Little exemple of deque.

```cpp
std::deque<int> my_deque(10,100);
std::deque<int>::iterator it;
my_deque.at(0) = 42;
my_deque[9] = 42;
std::cout << "Iterate through the deque" << std::endl;
std::cout << "First element of my deque :" << my_deque.front() << std::endl;
std::cout << "Last element of my deque :" << my_deque.back() << std::endl;
std::cout << "Deque capacity in elements:" << my_deque.size() << std::endl;
std::cout << "Deque maximum capacity in elements:" << my_deque.max_size() << std::endl;
std::cout << "Iterate through the deque" << std::endl;
for (it = my_deque.begin() ; it != my_deque.end(); ++it)
		std::cout << (*it) << std::endl;

```
### Associative containers
#### Set
Contains a sorted set of unique objects of a given type. Is implemented as [red-black tree](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree) 

```c++
int main()
{
	std::set<int> test;
	std::set<int>::iterator it;
	test.insert(2);
	test.insert(10);
	test.insert(12);
	test.insert(1);
	for (it = test.begin() ; it != test.end() ; ++it)
		std::cout << *it << std::endl;
}
```

#### Map
Contains a sorted container that contains key-value pairs with unique keys.
Is implemented as [red-black tree](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree) 
```c++
int main()
{
    std::cout << "Test map " << std::endl;
	std::map<std::string, int> test;
	std::map<std::string, int>::iterator it;

	test["SALUT"] = 10;
	test["AGE"] = 27;
	test["ANNE"] = 1997;
	test["JOUR"] = 20;

	std::cout << test["SALUT"] << std::endl;
	std::cout << test["AGE"] << std::endl;
	std::cout << test["ANNE"] << std::endl;
	std::cout << test["JOUR"] << std::endl;

	for (it = test.begin() ; it != test.end() ; ++it)
	{
		std::cout << it->first << ":" << it->second << std::endl;
	}

	std::cout << std::endl;
}
```
A map will not 
## Algorithms 

## Iterators
Templated iterators.

```c++
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

const_iterators
# Source
[[CPP - Source]]

## Recherche