# EX00
- [x] Use map container.
- [ ] input
	- [ ] second database storing different prices /dates to evaluate.
- [ ] Rules
	- [x] programm name is btc
	- [x] take a file as argument
		- [ ] check if the argument is a file or directory
	- [ ] Each line in this file must use the following format: "date | value"
	- [ ] Valid date have this format: YEAR-Month-Day.
		- [x] parse with '-' with geetline
		- [ ] check the validity of the 
			- [ ] year
			- [ ] month
			- [ ] day
	- [ ] A valid value must be either a float or a positive integer between 0-1000
Exemple of an input.txt
```txt
date | value
2011-01-03 | 3
2011-01-03 | 2
2011-01-03 | 1
2011-01-03 | 1.2
2011-01-09 | 1
2012-01-11 | -1
2001-42-42
2012-01-11 | 1
2012-01-11 | 2147483648
```

- [ ] get the closest lower date 
	- [ ] Leaf year between 2009 and 2022.
- [ ] Output is the value multiplied by the rate.

## Test
- [ ] Check the constructors
# EX02 
- [ ] Constraints
	- [ ] Executable PmergeMe
	- [ ] Positive integer sequence as arguments
	- [ ] Need to use the Ford-Johnson algorithm
	- [ ] Need to handle errors with message.
	- [ ] Use at least two different containers. (Implement the algorithm for each container.)
	- [ ] The program should handle 3000 different integers
- [ ] Hand
## Implementation
- [ ] Do the parsing
	- [ ] Check is positive integer.
	- [ ] Check is number.
	- [ ] Check if duplicate.


## Recherche
- [ ] How to create a binary tree.
- [ ] 