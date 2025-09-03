A thread is a flow of work that is executed in parallel. 
Thread programm can run on a uniprocessor.
The number of processor doesn't affect the programm structure.
## Definition

A new thread share the same ressource of the original one. 
Everything within a process is sharable among the threads in a process, including the text of the executable program, the program’s global and heap memory, the stacks, and the file descriptors.

## Some theory

When a thread is created, t**here is no guarantee** which will run first: the newly created thread or the calling thread.

When running a thread we need to sleep or wait the newly thread, if no the main thread might exit, thereby terminating the entire process before the newly process get a chance to run.
This behavior is dependent on the operating system’s threads implementation and scheduling algorithms.
## Thread creation

The thread creation is done with this function ``pthread_create`` here a small exemple that create a thread to execute the thread_hello function that can have mutilple arguments through the pthread_create args.

```c
void *thread_hello(void *args)
{
	t_arg *arg;
	arg = (t_arg*) args;
	if (write(1,&arg->salut,1) <= 0)
		perror("write");
	if (write(1,&arg->hoooo ,1) <= 0)
		perror("write");
	return (NULL);
}

int main()
{
	int p_id;
	pthread_t t_id;
	t_arg args;

	args.salut = 84;
	args.hoooo = 65;

	p_id = pthread_create(&t_id, NULL, thread_hello, &args);
	pthread_join(t_id, NULL); 
	return (0);
}
```

The pthread_join function is needed to wait for the termination of the newly created thread. We do it because we don't have any guarantee that the newly created thread will be executed before the termination of the main one.

## Thread termination

If in a thread an exit signal is sent. The process is then terminates thus all the thread are terminated.
The exemple below will print FROM HELLO2 and TA  but not FROM HELLO2 again.
```c
#include "threadtest.h"
void *thread_hello2(void *args)
{
	t_arg *arg;
	arg = (t_arg*) args;
	if (write(1,"FROM HELLO2" ,11) <= 0)
		perror("write");
	return ((void *) 12);
}

void *thread_hello(void *args)
{
	t_arg *arg;

	arg = (t_arg*) args;
	if (write(1,&arg->salut,1) <= 0)
		perror("write");
	if (write(1,&arg->hoooo ,1) <= 0)
		perror("write");
	exit(1); // The programm end here.
	return (NULL);
}

int main()
{
	int p_id; 
	pthread_t t_id[5];
	t_arg args;
	args.salut = 84;
	args.hoooo = 65;

	p_id = pthread_create(&t_id[1], NULL, thread_hello2, &args);
	pthread_join(t_id[1],NULL);
	p_id = pthread_create(&t_id[3], NULL, thread_hello, &args);
	pthread_join(t_id[3], NULL);
	p_id = pthread_create(&t_id[2], NULL, thread_hello2, &args);
	pthread_join(t_id[2], NULL);
	return (0);
}
```

## Different way to terminate
A single thread can exit in three ways, thereby stopping its flow of control, without terminating the entire process. 
1. The thread can simply return from the start routine. The return value is the thread’s exit code. 
2. The thread can be canceled by another thread in the same process. 
3. The thread can call pthread_exit. (TODO Explain this)

## Return value from routine

To return a value from a routine, its the second argument of pthread_join().
This code print FROM HELLO2, the value of tret is 12.
```c
void *thread_hello2(void *args)
{
	t_arg *arg;
	arg = (t_arg*) args;
	if (write(1,"FROM HELLO2" ,11) <= 0)
		perror("write");
	return ((void *) 12);
}

int main()
{
	int p_id; 
	pthread_t t_id[5];
	t_arg args;
	void *tret;

	args.salut = 84;
	args.hoooo = 65;

	p_id = pthread_create(&t_id[1], NULL, thread_hello2, &args);
	pthread_join(t_id[1],&tret);
	return (0);
}
```

If a thread is canceled the value return is PTHREAD_CANCELED.
### WARNING
If in a thread's stack you allocated some memory that you return, (Ex: you return a pointer to a structure.) The memory might be unavailable or changed by the time another thread reads it.

Exemple: This code will produce a segfault on Mac Osx., we can see that the first call of the structure is correct. But the another one made in the main thread is incorrect.
```c 
#include <pthread.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
struct foo
{
       int a, b, c, d;
};

void printfoo(const char *s, const struct foo *fp)
{
       printf("%s", s);
       printf(" structure at 0x%lx\n", (unsigned long)fp);
       printf(" foo.a = %d\n", fp->a);
       printf(" foo.b = %d\n", fp->b);
       printf(" foo.c = %d\n", fp->c);
       printf(" foo.d = %d\n", fp->d);
}
void *thr_fn1()
{
       struct foo foo = {1, 2, 3, 4};
       printfoo("thread 1:\n", &foo);
       pthread_exit((void *)&foo);
}
void *thr_fn2()
{
       printf("thread 2: ID is %lu\n", (unsigned long)pthread_self());
       pthread_exit((void *)0);
}

int main(void)
{
       int err;
       pthread_t tid1, tid2;
       struct foo *fp;
       err = pthread_create(&tid1, NULL, thr_fn1, NULL);
       if (err != 0)
              return (-1);
       err = pthread_join(tid1, (void *)&fp);
       if (err != 0)
              return (-1);
       sleep(1);
       printf("parent starting second thread\n");
       err = pthread_create(&tid2, NULL, thr_fn2, NULL);
       if (err != 0)
              return (-1);
       sleep(1);
       printfoo("parent:\n", fp);
       exit(0);
}
```
# Source
[[Note C/Source|Source]]