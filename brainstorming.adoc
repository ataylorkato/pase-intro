# Brainstorming:
- Shell definition: It's an interface to the operating system.

- working/current directory... talk about how cd'ing from one directory and trying to access a file in the previous directory will not work.

- Go into details of the ls command.  Simple ls.  ls with -a option.

- find command.  (what about 'locate'?)

- Show how to use wildcards.  ? is any single character.  * is any amount of characters.  Create set of files so they can do wildcards like *e*.  Also called "globbing".

- Relative path names i.e. ./ ../   Can relate to above working directory cd by doing a "ls ../prevdir"  Two dots means "parent of this directory".  A universal way to get to the directory above the current one.

Talk about the /home/user dir, also using ~ as a shortcut.  The ~ "expands" out the single character and replaces it with /home/<user>.  Aka, expansion.

cd - (minus) will return you to the directory before the most recent cd.

I/O.  Stream of characters.  Standard Input and Standard Output and Standard Error.

Piping is like picking *DISPLAY or *PRINT for output.  You can immeidately act on the output.

Foreground/background jobs.  Background uses & and release control of the terminal.

Write first shell script.  #!/usr/bin/bash.  Talk about . (dot) for sourcing to current process.  chmod +x script

TODO
- does the 'jobs' command exist in PASE?