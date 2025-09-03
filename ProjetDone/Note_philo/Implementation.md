There are many forks as philosopher.
Every philosophers must be an thread.
Philosopher don't know if another philosopher is about to die.
Philosopher cannot speak with each other so the thread cannot join between them.
## Args
- number_of_philosophers : The number of philosopher and forks
- time_to_die (in miliseconds) : The time from the beginning of the simulation or the last meal they can live.
- time_to_eat (in miliseconds) : The time a philosopher will eat thus hold 2 forks.
- time_to_sleep (in miliseconds): The time a philosopher will sleeping.
- number_of_times_each_philosopher_must_eat (optional argument)
## Outputs
- Every state change.
- The state change format. **X is the name of the philosopher**
	- timestamp_in_ms X has taken a fork | is eating | is sleeping | is thinking | died


## Philosopher actions
- EAT : While eating cannot think or sleep
- THINK : While Thinking cannot eating or sleeping
- SLEEP : While sleeping cannot eating nor thinking.
- DIE : It's the end of the road.

### Eating
- Need two fork to eat.
- One on they right the other on the left.
- After eating the philosopher put the fork back and goes to sleep

### Sleeping
- Sleep after eating.
### Thinking
- After sleep thinking or if not able to eat.

## Philosopher number
- Begin at 1
- End at number_of_philosopher.
- Philosopher number 1 sits next to philosopher number_of_philo.
- Any other philo Number N sit between Philo  number N-1 and philo  number N+1
## End of the simulation
- A philospopher d**ies if they didn't start eating time_to_die ms since the last meal or the beginning of the simulation.**
- If the number_of_times_each_philosopher_must_eat is not set, **the simulation end when a philosopher dies**
- If the number_of_times_each_philosopher_must_eat i**s set the simulation end when all the philosopher have eaten at least X number of times.**
- The message that a philosopher has died have to pop maximum **10ms after the death**

## What a philo know
- Time to eat
- Time to sleep
- That it should take 2 fork for eating.
- What is its number
## What the server know
- Which philo is which
- Where to put philo.
- If a philo is dead/or if they all eat the correct number of times.
- Printing messages.

# NOte
faire philo[i].right_fork = philo [ i % nbr_total_philo].left_forks.