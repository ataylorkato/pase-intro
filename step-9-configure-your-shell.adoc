# Configure Your Shell

When you first log in there are default files run before the command prompt is displayed.  The file is different depending on which shell you are using.  For example, this lab is using `zsh` so the file looked at is `.zprofile`.  If we were using `bash` it would look for `.bash_profile` or `.profile`. Think of this being similar to the `INLPGM` parameter on `CRTUSRPRF`.

The `.zprofile` file is located in the user's home directory, as shown below.

```
~% ls -al ~/.zprofile
-rwx------    1 usrmah25 0               304 Apr 14 22:21 /home/USRMAH25/.zprofile
```

Now display the contents of `~/.zprofile` using the `cat` command.

```
~% cat ~/.zprofile
TERM=xterm
umask go=
export LITMIS_SPACE_GUID=I7EDN
export LITMIS_SPACE_USER=USRMAH25
export LITMIS_SCHEMA_DEVELOPMENT=I7EDN_D
export LITMIS_SCHEMA_TEST=I7EDN_T
export LITMIS_SCHEMA_PRODUCTION=I7EDN_P
export LITMIS_PORT_DEVELOPMENT=62883
export LITMIS_PORT_TEST=62884
export LITMIS_PORT_PRODUCTION=62885
```

Here we see a number of environment variables being set (i.e. `TERM`, `LITMIS_SPACE_GUID`, etc) and also the [`umask`](http://www.computerhope.com/unix/uumask.htm) command being run.   Environment variables hold values that can be made available to any program in this shell session.  Think of them as being similar to an IBM i https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_73/rbam6/lclda.htm[Local Data Area (*LDA)], a place to hold data that is specific to this job.

All of these environment variables are set once you log in.  You can see their values at any time using the `echo` command.  Try running the below command.

```
~% echo $LITMIS_SPACE_GUID
I7EDN
```

As you can see it displayed the value stored in `LITMIS_SPACE_GUID`.

## Try: Changing The Prompt via `.zshrc`

Another file that is invoked at login is `.zshrc`.  We can add a line in here to modify what the prompt looks like in the event we aren't satisfied with the default.  For example, by default the prompt looks like the following.

```
[usrmah25@SPACES]~%
```

**NOTE:** Remember that for the sake of brevity this lab has been using `~%` vs. `[usrmah25@SPACES]~%`.
What if we wanted that to be more colorful and not just black and white? We can easily change the colors of the prompt but first we need to test the command we need to run to make those changes.

Type the following into the shell.

```
print -P '%B%F{red}co%F{green}lo%F{blue}rs%f%b'
```

You should see a result similar to the below screen shot.

image:/assets/zsh_colors.png[alt=""]



Here's what those %'s followed by letters mean.
[width="10%"]
|=======
|%B(%b) |Start (stop) boldface mode.
|%F (%f) | Start (stop) using a different foreground colour,
|=======

So basically it's giving us a way to delimit strings in the prompt and apply markup to them (i.e. change colors, bolding, etc).  

**NOTE:** If you like you can visit the http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html[zsh documentation] for more information on the variety of values that can be specified.

Now run the following `print` statement.

```
print -P '%F{red}%n%f@%F{blue}%m%f %F{yellow}%1~%f %# ' 
```

You should now see something similar to the following.

image:/assets/zsh_colors_user.png[alt=""]

A couple of new `%` values were introduced that are detailed in the below table.

[width="10%"]
|=======
|%n | Pulls value from `$USERNAME`
|%m | The hostname up to the first period (`.`).
|%1 | Trailing component of the current working directory.
|=======


We're using the `print` command to quickly test output to learn what we want our prompt to look like. Now it's time to apply this new shell prompt format permanently.  

Instead of using `joe` to create and occupy `.zshrc` we will instead use a short-cut.  Paste the following into a shell session.

```
~% echo "PROMPT='%F{red}%n%f@%F{blue}%m%f %F{yellow}%1~%f %# '" > ~/.zshrc
```

The `echo` command will process the string and instead of directing the output to the screen the `>` symbol declares to redirect it to file `~/.zshrc`.

Run the below `cat` command to make sure everything worked.

```
% cat ~/.zshrc
PROMPT='%F{red}%n%f@%F{blue}%m%f %F{yellow}%1~%f %# '
```

At this point the prompt changes still haven't taken effect because file `.zshrc` is only process when a new shell is created.  You can either close the browser tab and open it again from the Litmis Spaces dashboard or simply type `zsh` to start a new shell session, as shown below.

image:/assets/zsh_final_color_prompt.png[alt=""]

**Success!**

## Please proceed to the next step.