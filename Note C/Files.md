fopen opens the named file, and returns a stream, or NULL if the attempt fails. Legal values for mode include:

open text file for reading  
create text file for writing; discard previous contents if any append; open or create text file for writing at end of file
- "r"  
- "w"  
- "a"  
- "r+" open text file for update (i.e., reading and writing)  
- "w+" create text file for update, discard previous contents if any "a+" append; open or create text file for update, writing at end
## Get info

```
man 2 open
man 2 read
man 2 close
man 2 write
```
## Files descriptors
The number the OS uses to keep track of open files.
- 0 -> standard input
- 1 -> standard output
- 2 -> standard error
## fopen vs open
- fopen is a library function. 
- open is a system call.
Open is less portable can be find on linux, macOS or POSIX system.

Mode with open:

### fopen
fopen returns a pointer to a file
```
FILE *
```

### open
open return an int that is a file descriptor, it is taken in the first available fd table.
It takes the name of the file , FLAG.
Exemple: In this exemple we "open" a file name CAMION and `write` TIME in it
```c
int main()
{
    int fd = open("CAMION",O_WRONLY | O_TRUNC | O_CREAT);
    int x = write(fd,"TIME",4);

    if (x < 0)
        perror("file camion");
    return (0);
}
```
- O_WRONLY : Open the file in write only
- O_TRUNC: if the file exist and have the correct writing right (O_WRONLY) then the lenght is put to 0
- O_CREAT : if the file doesn't exist create it.
### close
Close a file descriptor
```
close(int_fd);
```

### read
read nbytes of the file descriptor inside a buffer.
Every time you call read continue where it stops if it didn't read all the file.
If read read all the file in one call. The buffer is not changed but return value is 0.

## Source
[[Source]]
