## Simple Shell
---
  
#### Table of contents
- [Context](#context)
- [How the Shell Works](#how-the-shell-works)
  - [Oversimplied](#oversimplified)
  - [simplified](#simplified)
  - [Framework with example](#framework-with-example)
- [Compilation]
- [Memory](#memory)
- [Functions Overview](#functions-overview)

---
  
#### Context:  
  
A simple UNIX command interpreter, enter your code and see what it does.
  
[^](#table-of-contents)
  
---

#### How the Shell Works
  
#### Oversimplified:

READ -> PARSE -> EXECUTE -> LOOP
  
[^](#table-of-contents)
  
---

### Simplified
  
- Enter terminal
- User inputs command line
- Read line
- Examine and parse line into commands
- Check if commands already integrated in shell
- If yes, output, back to 2nd line
- If no, continue
- Look into every directory in PATH to see if command exists and is available
- If yes, output, back to 2nd line
- Fork, Shell duplicates into 2 processes: Parent and Child
- Child becomes command line
- Parent waits for Child to execute command
- Free dynamic memory
- Back to 2nd line
  
[^](#table-of-contents)
  
---
  
#### Framework with example:  
  
for the "ls -l" command
  
1. main.c  
-----> START  
-----> isatty() -----> prompt ($)  
-----> getline() ----> read "ls -l"  

2. utils.c  
-----> strtok() -----> parse "ls -l"  
-----> args = ["ls", "-l", NULL]  

3. builtins.c  
-----> strcmp (args[0], "exit") -----> if YES back to START  
-----> strcmp (args[0], "env") ------> if YES back to START  

4. path.c  
-----> getenv("PATH")  
-----> access("/bin/ls", X_OK)  
-----> return "/bin/ls"  

5. shell.c  
-----> fork()  
-----> CHILD -----> execve("/bin/ls", args, environ)  
-----> PARENT ----> wait (NULL)  

6. main.c  
-----> prompt ($)  
-----> back to START  
  
[^](#table-of-contents)

--- 

#### Functions overview

access()
execve()
exit()
fork()
free()
getenv()
getline()
getpid()
isatty()
strcmp()
strtok()
wait()
  