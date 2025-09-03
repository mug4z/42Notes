Variable qui ne se détruise pas out of scope.

Exemple 
```c
#include <stdio.h>

int ft_test_static(void)
{
	static int i=0;
	i++;
	return (i);
}
int main()
{
	printf("%d",ft_test_static());
	printf("%d",ft_test_static());
	printf("%d",ft_test_static());
	printf("%d",ft_test_static());
	printf("%d",ft_test_static());
	printf("%d",ft_test_static());
}
```
**Output** -> 123456

Les variables static sont allouer dans le data segment de la mémoire.

Les variables static comme les variable globales sont initializer a 0 si pas initialiser explicitement. Le code suivant va générer des erreurs.
Exemples:
```c
int main()
{
	static int x;
	int y;
	printf("%d \n%d",x,y);
}
```
Output:
	0
	some_garbage_value

Les variables static ne peuvent être uniquement initializer avec des literal constant. Le code suivant ne compile pas
Exemples:
```c
#include<stdio.h>
int initializer(void)
{
	return 50;
}

int main()
{
	static int i = initializer();
	printf(" value of i = %d", i);
	getchar();
	return 0;
}
```
Output:
```
test_static_variable.c:9:17: error: initializer element is not a compile-time constant
        static int i = initializer();
                       ^~~~~~~~~~~~~
1 error generated.
```
# Source
[[Note C/Source|Source]]