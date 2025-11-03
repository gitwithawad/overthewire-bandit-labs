# NOTES:

- The aim of this level is to find the password for the next level that is in a file within the **inhere** directory that has the following properties:
1. human-readable 
2. 1033 bytes in size
3. not executable

- so the commands that could be used in this file are the following:
  - ls = list of directory contents 
  - cd = navigate through directories 
  - cat = concantonate files and print a standard output 
  - file = determine file type
  - du = estimate file space usage (stroage of a file)
  - find = search for files in a directory hierarchy
 
- I found out that all the others ownerships in the list of the **inhere** directory are **not executable** but using the ls -l and by using ls -la to later find that one directory (called ..) is executable
- However, the .. directory is the only human readable directory so I navigated there only to them realise that you cannot access .. as that takes you back to the parent directory of the current one.
- So it took me back to **bandit5** directory
- when using du, which also checks the size of directory, i found out an option called -h or --human-readable which displays sizes in human-readable format
- I also found out that the grep command is used for filter
  
- Now I couldn't find out on my own but with research I realised with just using these commands that I mentioned above I can find out the answer:

  - I used the find command by using the opition size now the way I used it was:
*find /home/bandit5/inhere -size 1033* and *find /home/bandit5/inhere +size 1033*

  - But then with research I should have done the same command but with one more option which was the type option
  - this helps to find what kind of filesystem object to look for, so f is for file and d is for directory
  - in this case I used f
  - also I used a unit for the number in size
  - as without it, it would look for the blocks of bytes
  - so i used c to just find out the bytes
  - so the command looked like this:
  *find /home/bandit5/inhere -type f -size 1033c*
  - which gave me the output of this:
  */home/bandit5/inhere/maybehere07/.file2*
 
  - I also found out that you can use cat to print out files in a path
  - So in this case, I used the command cat to print the path above like this:
  *cat /home/bandit5/inhere/maybehere07/.file2*
  - Which finally gave me the result which was:
    **HWasnPhtq9AVKe0dmk45nxy20cvUa6EG**

## what I learnt is:
- ### As a beginner, coding will look messy but the result is worth it
- ### I need to get used to these options to certain command
- ### I can always restart to the beginning for help and take my time
