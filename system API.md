# System API

## Table of contents

## [system](https://www.tutorialspoint.com/c_standard_library/c_function_system.htm)

> The C library function int system(const char *command) passes the command name or program name specified by command to the host environment to be executed by the command processor and returns after the command has been completed.  


```
#include <stdio.h>
#include <string.h>

int main () {
   char command[50];

   strcpy( command, "ls -l" );
   system(command);

   return(0);
} 
```