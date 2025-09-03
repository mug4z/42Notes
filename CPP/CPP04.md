## Ex00
- [x] Class Animal
- [x] Class Dog
- [x] Class Cat 
- [x] Wrong Cat 
- [x] Wrong Animal

## Ex01
Chercher comment faire pour que Cat depuis Animal je puisse setter des ideas.
- [x] Class Brain
	- [x] getter
	- [x] setter
- [x] Add Brain* into cat
	- [x] getter for brain
	- [x] setter for brain
- [x] Add Brain* into Dog
	- [x] getter for brain
	- [x] setter for brain
- [x] Add delete brain into destructor Cat
- [x] Add delete brain into destructor Dog

- [x] Make sure to do deep copy of Dog and Cat.


## Ex03
- [x] AMateria abstract class
	- [x] Materias class 
		- [x] Ice
			- [x] Type ice
			- [x] copy constructor;
		- [x] Cure
			- [x] type cure
			- [x] copy constructor
- [x] Character class
	- [x] Use the interface ICharacter
	- [x] Constructor with name 
	- [x] Any copy of Character needs to be deep.
	- [x] During copy the Materias of a character must be deleted before new ones are added.
	- [x] Materias must be deleted when a character is destroyed.
- [x] Class floor.
- [ ] MateriaSource class
	- [ ] Learn materia: copies a meteria and store it in memory, at most 4 Materias.
	- [ ] CreateMateria : returns a new materia it is a copy of a materia previously learn.
	- [ ] return 0 if the type is unknown.