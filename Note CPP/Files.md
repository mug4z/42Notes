## Open files 
1. Create a stream
```c++
ifstrean file("fileName"); // input stream
```
- If the file cannot be open the file variable will be false.
## Closing files
```c++
file.close()
```
## Create file
```c++
ofstream out("filetobecreated");
```
- If the file is already created it will erase its content.
- It will fail if a folder is already there with the same name of your file.