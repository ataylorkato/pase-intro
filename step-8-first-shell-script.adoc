# First Shell Script

**Shell scripts are the CL of PASE.**  For example, sometimes you'll front an RPG program with a CL program to prime the environment (i.e. `OPNQRYF`).  Or other times you'll want to combine a bunch of CL commands into an easily callable program.  Shell scripts serve the same purpose. However, one important difference is that shell scripts are **not** compiled.

A shell script is stored in a text file, usually with a `.sh` extension, though no extension is necessary; it's the content that is important.

Use `joe` to create `first.sh`, as shown below.

```
~% joe first.sh
```

Add this single line to `first.sh` and use `Ctrl` + `X` to save and exit.

```
echo 'hello'
```

Now invoke `first.sh` by typing it by name on the command line and pressing `Enter`.

```
~% first.sh
zsh: permission denied: ./first.sh
```

The shell, `zsh`, is telling us we don't have execute permission.  Use the `ls -al` command to check the permissions.

```
~% ls -al first.sh
-rw-------    1 usrmah25 0                12 Apr 26 16:28 first.sh
```
We've not discussed file system permissions yet so this output doesn't mean much to you.  In this case we're interested to see if the owner (you) has execute (`x`) authority to this file.  The owner permissions are shown in positions 2,3, and 4.  We can see `rw-` in those positions which means the owner has r=read and w=write permissions but **not** x=execute permission.

Use the `chmod` command to add execute permissions for the owner, as shown below.

```
~% chmod +x first.sh
~% ls -al first.sh
-rwx------    1 usrmah25 0                12 Apr 26 16:28 first.sh 
```

As you can see the owner now has `rwx` permissions.  Try invoking `first.sh` again.

```
~% first.sh
hello
```

**Success!!**

Next rename `first.sh` to be `first`, essentially removing the `.sh` extension. 

```
~% mv first.sh first
```

Now invoke the shell script again using the new name.

```
~% first
hello
```

**Success!!**

## Try: Passing Parameters 

When writing RPG or CL programs it is very common to pass inbound parameters.  Shell scripts have the same need.  Let's change the `first` program script to receive two parameters.

Open the `first` file with `joe`.

```
~% joe first
```
 
Change the `echo` line to the following. 

**NOTE:** Short-cut keys like `Ctrl` + `E` (go to end of line) work inside the `joe` editor.

```
MSG="hello $1. Your last name is $2"
echo $MSG
```

As you can see we introduced `$1` and `$2` which are known as positional parameters.  These will contain the first and second parameters passed from the command line. The `MSG` variable was also introduced and is storing the resulting string.  Note that when we assign values to shell variables we don't include the `$` symbol and when we access the shell variable we include the `$` symbol.  This tells the shell interpreter to use the variable's value instead of the variable's name.  Said another way, the `$` is **not** part of the variable name and instead declares to the shell to _"insert the variable's content here"_.

Invoke the `first` script and pass in your first and last name, as shown below.

```
~% first Aaron Bartell
hello Aaron. Your last name is Bartell
```

As you can see the `$1` was replaced with `Aaron` and `$2` was replaced with `Bartell`.

### Try: Perl As Script Runtime

We can tell the shell interpreter to not assume the contents of a script are shell commands.  In fact, we can tell it the contents are a completely different programming language, like Perl!

Edit the `first` file and place the below contents into it.  This is essentially a Perl hello world program.

```
#!/QOpenSys/QIBM/ProdData/OPS/tools/bin/perl                                    
                                                                                
use strict;                                                                     
use warnings;                                                                   
                                                                                
print "Hello Perl!\n";
```

The first line in the program is called the https://en.wikipedia.org/wiki/Shebang_(Unix)[Shebang]

It's important to note lines 3,4, and 6 are Perl syntax and the shell doesn't know how to interpret them.  Instead it looks at the Shebang line (if one exists) to determine what interpreter should be loaded to process the remainder of the file.

Now try running the `first` program again, as shown below.

```
~% first
Hello Perl!
```

**Success!**

As you can see it successfully engaged the Perl interpreter to process the lines of Perl code.  You might ask **"why not just run `perl first`?**.  The cool thing about adding the Shebang approach is that it _feels_ like a command is being used and actually takes less key strokes to invoke.

## Please proceed to the next step.