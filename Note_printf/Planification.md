## Recherche
- Makefile call another makefile ? -> [Recursion make](https://www.gnu.org/software/make/manual/make.html#Recursion)
- Varidadic function -> OK
	- va_start, va_arg, va_copy, va_end -> juste va_copy a voir.
- Formated output ? -> a lire https://www.gnu.org/software/libc/manual/html_mono/libc.html#Formatted-Output

Output : libftprinft.a
External functions : malloc, free, write, va_start, va_arg, va_copy, va_end

## Implementation
- Valeur de retour a voir, un int, le nombre de character printé sans compter `\0`
- Logique boucle sur la string, quand il y a un `%d` prendre la bonne conversion.
	- Pattern a trouver `%type conversion`
### Planification implementation
Ajouter la gestion si write erreur write renvoie -1
1. Parse the string given in first argument.
	1. Test en convertissant l'addresse de mon premier argument variable en long et en le donnant a ma fonction ft_convert_hex si sa marche. -> OK
2. Implement the %p conversion. -> [[%p conversion.canvas|ft_printf schema]] 
	3. Ajouter le 0x en prefixe. -> OK
	4. Ne pas print le %p.  ->  OK
	5. la valeur de retour de mon printf doit suivre,  -> OK
3. Implement the %c and %s conversion. -> OK
4. Implement the %d and %i and %u conversion. 
	1. Changer 
5. Implement the %x and %X conversion. 
	1. Conversion en %x minuscule done.
6. Implement the `%%` conversion.

Requirements:
- Don’t implement the buffer management of the original printf().
- Your function has to handle the following conversions: cspdiuxX% 
- Your function will be compared against the original printf(). 
- You must use the command ar to create your library. Using the libtool command is forbidden. 
- Your libftprintf.a has to be created at the root of your repository.
Implementation :
- %c Prints a single character. 
-  %s Prints a string (as defined by the common C convention).
-  %p The void * pointer argument has to be printed in hexadecimal format. 
-  %d Prints a decimal (base 10) number. 
-  %i Prints an integer in base 10. 
-  %u Prints an unsigned decimal (base 10) number.
-  %x Prints a number in hexadecimal (base 16) lowercase format. 
-  %X Prints a number in hexadecimal (base 16) uppercase format. 
-  %% Prints a percent sign

