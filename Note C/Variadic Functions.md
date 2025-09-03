It is a function that can take any number of parameters.

You need `#include <stdarg.h>` to parse argument in variadic function.

Prototype exemple : `int ft_varsum(int count, ...)`
- You need to have at least one named argument it's a standard requirement, here count.
- The '...' are called ellipsis and this what contain all the argument after count.
- The only way to access them is sequentially, in the order they were written. You must use the special macros from stdargh.h

```c
int ft_varsum(int count, ...) // Avoir le premier arguement est une requierement du standard C
{
    int i;
    int res;
    
    va_list args; // Creer une variable de type va_list
    va_start(args,count); // Premier argument apres count, si args n'est pas un va_list erreur

    i = 0;
    res = 0;

    while (i < count)
    {
        res += va_arg(args, int); // Donne succesivement le premier argument optionel et le suivant et ainsi de suite.
        i++;
    }

    va_end(args); // Pas besoin de le mettre avec gcc mais le mettre augmente la compatibiliter avec d'autre compiler

    return res;
}


int main()
{
    ft_varsum(3,1,2,3);
}
```


### Summary

1. Create a va_list variable
2. va_start(va_list variable, the given argument), setup the first optional argument
3. va_args(va_list variable, the type to return), get the arguement one by one by successively call it.
4. va_end(va_list variable), indicate you are finished.

You can declare different va_list variable for the same set of arguments.
# Source
[[Source]]