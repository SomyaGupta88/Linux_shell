# Linux_shell
**To install the readline library, Open the terminal window and write**  
`sudo apt-get install libreadline-dev`  
 
**It will ask for your password. Enter it. Press y in the next step.**  
- Printing the directory can be done using **getcwd**.
- Getting user name can be done by **getenv(“USER”)**
- Parsing can be done by using **strsep(“”)**. It will separate words based on spaces. Always skip words with zero length to avoid storing of extra spaces.
- After parsing, check the list of built-in commands, and if present, execute it. If not, execute it as a system command. To check for built-in commands, store the commands in an array of character pointers, and compare all with **strcmp()**.
Note: “cd” does not work natively using execvp, so it is a built-in command, executed with chdir().
- For executing a system command, a new child will be created and then by using the execvp, execute the command, and wait until it is finished.
- Detecting pipes can also be done by using **strsep(“|”)**.To handle pipes, first separate the first part of the command from the second part. Then after parsing each part, call both parts in two separate new children, using execvp. Piping means passing the output of first command as the input of second command.  
  - Declare an integer array of size 2 for storing file descriptors. File descriptor 0 is for reading and 1 is for writing.
  - Open a pipe using the pipe() function.
  - Create two children.
  - In child 1->  
  `Here the output has to be taken into the pipe.
Copy file descriptor 1 to stdout.
Close  file descriptor 0.
Execute the first command using execvp()`  
  - In child 2->  
`Here the input has to be taken from the pipe.
Copy file descriptor 0 to stdin.
Close file descriptor 1.
Execute the second command using execvp()`
  - Wait for the two children to finish in the parent.  
  
**To Run the code –**  
`gcc shell.c -lreadline`  
`./a.out `
