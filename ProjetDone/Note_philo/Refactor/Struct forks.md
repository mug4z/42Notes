The struture will be like

```c
typedef struct s_l_fork
{
	pthread_mutex_t	l_fork;
	int				last_used;
}				t_l_fork;

typedef struct s_r_fork
{
	pthread_mutex_t	*r_fork;
	int				last_used;
}				t_r_fork;

typedef struct s_forks
{
	t_r_fork	*p_r_fork;
	t_l_fork	*p_l_fork;
}			t_forks;

typedef struct s_philo
{
	t_info			*info;
	int				philo_id;
	t_forks			*forks;
	int				state;
}				t_philo;
```

Functions to refactor
- clean forks -> OK
- init_l_forks -> OK
- inti_r_forks -> OK
- set_r_forks -> OK
- set_l_forks -> OK
Apply changes -> OK
fork_assigment vraiment besoin ?

refactor
	- init_r_forks
	- set_r_forks
	- clean forks