ATTENTION si on initialize mal des mutex, on peut avoir un segfault mais a la fin du programme ???!!!!
## Definition
Mutex stand for, mutual-exclusions.

A mutex is basically a lock that we set (lock) before accessing a shared resource and release (unlock) when we’re done.
When a thread lock a ressources, other thread have to wait the unlock to access the ressources.
## Exemple

Exemple: This code will increment arg->salut to 300000 if you don't protect the incrementation without mutex the incrementation is undefine thus it will be a different number everytime you run the code.
```c
#include "threadtest.h"

void *addone(void *args)
{
	t_arg *arg;
	int status_lock;
	int status_unlock;

	arg = (t_arg *) args;
	status_lock = pthread_mutex_lock(&arg->lock);

	printf("Status lock %d\n",status_lock);
	int index = 0;
	while (index < 100000)
	{
		arg->salut += 1;
		index++;
	}
	status_unlock = pthread_mutex_unlock(&arg->lock);
	printf("Status unlock %d\n",status_lock);
	return (NULL);
}

int main()
{
	
	int p_id, p_id2, p_id3, status_mutex_init;
	pthread_t t_id, t_id2, t_id3;
	t_arg args;

	args.salut = 0;
	
	printf("Before increment %d\n",args.salut);
	status_mutex_init = pthread_mutex_init(&args.lock, NULL);
	p_id = pthread_create(&t_id, NULL, addone, &args);
	p_id2 = pthread_create(&t_id2, NULL, addone, &args);
	p_id3 = pthread_create(&t_id3, NULL, addone, &args);

	pthread_join(t_id, NULL);
	pthread_join(t_id2, NULL);
	pthread_join(t_id3, NULL);
	pthread_mutex_destroy(&args.lock);
	printf("After increment %d\n",args.salut);
	return (0);
}

```


### pthread_mutex_unlock
Calling pthread_mutex_unlock() with a mutex that the calling thread does not hold will result in undefined behavior.

### pthread_mutex_destroy
Must be executed before freeing the mutex.
## Deadlock
A thread will deadlock itself if it tries to lock the same mutex twice.
You’ll have the potential for a deadlock only when one thread attempts to lock the mutexes in the opposite order from another thread.
# Source
[[Note C/Source|Source]]