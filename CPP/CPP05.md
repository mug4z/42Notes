# EX00

- Bureaucrat
	- constant name -> Done
	- grade from 1 to 150 -> Done
	- getter for name and grade -> OK
		- getName() and getGrade() -> OK
	- exception to be thrown -> OK
		- Bureaucrat::GradeTooHighException -> OK
		- Bureaucrat::GradeTooLowException -> OK
	- Implement function to increment and decrement grade  -> OK
		- Since grade 1 is the highest one and 150 the lowest, incrementing a grade 3 should give a grade 2 to the bureaucrat. _> OK_
	- overload the << operator to print a message like this -> Done
		- [name], bureaucrat grade [grade] -> Done
- Main
	- Write tests -> DONE
	- 

## Recherche
- Exception in CPP ?
	- try catch block
- Exception classes ?
- Custom exceptions

# EX01
prendre une bureaucrat verifie les infos et sign si ok.

- Form
	- These attributes are PRIVATE
	- constant name -> OK
	- Boolean indicating it is signed -> OK
	- A constant grade to sign it -> OK
	- A constant grade to excecute it -> OK
- exception to be thrown -> OK
	- Form::GradeTooHighException -> OK
	- Form::GradeTooLowException -> OK
- getter and setter -> OK
-  overload the << operator to print a message like this -> OK
	- print all forms information
- Add condition  that sign grade must not be smaller than excecute. -> OK
- member function 
	- besigned() take a bureaucrat as paramter. -> OK
		- change the form status based on the grade of the bureaucrat is higher or egal. -> OK
		- if the grade is toolow GradeTooLow Exception -> OK
	- signForm() to the bureaucrat. -> OK
		- if the form go signed it will print something like -> OK
			- [bureaucrat] signed [form]
			- otherwise [bureaucrat] couldn’t sign [form] because [reason].
- Do the test for copy constructor -> DONE
# EX02
- [x] The execute function
	- [x] Check that the form is signed and that the grade of the bureaucrat that execute it is high enough.
	- [x] Create an function in AForm to check that.
	- [x] throw an execption if not enough grade. or not signed.
- [x] Transform Form into abstract class 
	- [x] The attributes need to remain private
	- [x] The execute member pure virtual
- [x] ShrubberyCreationForm
	- [x] Required grades: sign 145, exec 137
	- [x] Create a file [target]_shrubbery in the working directory, and writes ASCII trees inside it.
	- [x] take target in constructor.
	- [x] Write tests
		- [x] Failed
- [x] RobotomyRequestForm
	- [x] Required grades: sign 72, exec 45
	- [x] Makes some drilling noises. Then, informs that [target] has been robotomized successfully 50% of the time. Otherwise, informs that the robotomy failed
	- [x] take target in constructor.
	- [x] Write tests
- [x] PresidentialPardonForm
	- [x] Required grades: sign 25, exec 5
	- [x] Informs that [target] has been pardoned by Zaphod Beeblebrox.
	- [x] take target in constructor.
	- [x] Write tests
- [x] Add executeForm(AForm const & form) to the bureaucrat.
	- [x] Testit with Shruberry
	- [x] Test it with Robo
	- [x] Test it with Presidential

# EX03
DONT USE IF ELSE ELSEIF forest
- [ ]  Intern class
	- [x] makeform member
		- [x] Two strings 1 name of a form 2 target of the form.
		- [x] "robotomy request"
		- [x] "president pardon"
		- [x] "shrubbery creation"
		- [x] return a pointer to a form obkect
	- [x] Print something like
		- [x] Intern creates [form]
		- [x] Print an error if the form doesn't exist
		- [ ] 
