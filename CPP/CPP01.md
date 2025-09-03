 ## EX00

- Private attribute Name -> OK
- Add a member function announce -> OK
- Implements Zombie* newZombie( std::string name ); -> OK
- Implements void randomChump( std::string name ); -> OK

Search
How to use the new keyword;
When it is best to allocate memory on stack or heap ?

##  EX01

- Implement Zombie* zombieHorde( int N, std::string name ); -> done

## Ex02
- print:
	- The memory address of the string variable. -> OK
	- The memory address held by stringPTR. -> OK
	- The memory address held by stringREF -> OK
	- The value of the string variable. -> OK
	• The value pointed to by stringPTR. -> OK
	• The value pointed to by stringREF. -> OK
## Ex03
- Weapon class
	- A private attribute type, which is a string -> OK
	- A getType() member function that returns a const reference to type. -> OK
	-  A setType() member function that sets type using the new one passed as parameter -> OK
- HumanA and HumanB
	- both have a weapon and name -> OK
	- function attack() -> OK
- HumanA take the Weapon in its constructor, not HumanB -> OK 
- HumanB may  not always have a Weapon, whereas HumanA will always be armed.
- TEST code
```c++
int main()
{
	{
		Weapon club = Weapon("crude spiked club");
		HumanA bob("Bob", club);
		bob.attack();
		club.setType("some other type of club");
		bob.attack();
	}
	{
		Weapon club = Weapon("crude spiked club");
		HumanB jim("Jim");
		jim.setWeapon(club);
		jim.attack();
		club.setType("some other type of club");
		jim.attack();
	}
return 0;
}

```

## Ex04
- Test Input file
	- Check if input file exist
	- Check if input file is a folder
	- Check if it can be read.
- Test Output file
	- Check if output file already exist
	- Check if the outputfile can be writen to.
- Arguments 
	- argv[1] -> filename
	- argv[2] -> S1
	- argv[3] -> S2
- Goal
	- Replacing every occurrence of S1 with S2.

## Ex05 -> DONe

## Ex06

