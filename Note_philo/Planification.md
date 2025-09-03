 - [x] faire un gitignore.
## Functions
- [x] Add the ft_calloc.
## Add check for the argument:
- [x] Number is not more than int max cannot be tested as the limit of ft_itoa is int.
- [x] Number cannot be zero
- [x] Is not a number
- [x] Numbers cannot be negative.
### Leaks
- [x] Check for leak.s

## Initialize the timer
The gettimeofday should be starting a the begining of programm and be the reference for every other thread.
- [x] init the timer
- [x] Function that convert struct timeval into seconds.
- [x] Make a function that convert time elapsed since the beginning of the programme.

## Initialize of the shared info
- [x] Init ref_time_of_day
- [x] Init time_to_die
- [x] Init time_to_eat
- [x] Init time_to_sleep

## Initialisations
### Init philo_id
- [x] Add the philo_id.
### Init fork
- [x] Create a table of mutex representing the fork.
- [x] Put all the init function into one big so the main remain clean.
- [x] The address is not well set in the init_philo_id function.
	- [x] The issue was on the way I freed the memory.
- [x] Check for leaks and do the cleaning functions.
	- [x] PHILO, 
	- [x] GENERAL_INFO,
	- [x] FORKS -> TODO
- [x] Link the fork table with the structure, in relation to the philo_id.
- [x] init the right fork.
- [x] tester la protection.
- [x] Update the struct of rules in array of rules.
- [x] Refactor the forks struct. To make sure to have a structure like this
### Subroutine (Philosophers)
- [x] Create philo in function
- [x] Changer thread_create et ajouter la logique que les pair commence avec le statue eat et impair sleep.
- Call the functions (Array of functions pointer ?)
	- [x] take the fork
	- [x] setter d'abord quell philo peut manger quoi. avec un flag dans la structure des fourchette qui indique quelle philoid peut manger ave ces fourchettes. -> OK
	- [ ] eat
	- [x] sleep
	- [x] think
	- [x] With odd number of philo the last one take his fork but not the other fork and in the first round.
	- [ ] make sure you have nothing shows up with -fsanitize=thread
	- [x] QUIT properly when a philo dies
	- [ ] Make the condition for the optional argument
# !!ATTENTION!! 
NE PAS OUBLIER L'ARGUMENT OPTIONEL