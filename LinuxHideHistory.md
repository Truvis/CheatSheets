## Bash history
Bash maintains the list of commands internally in memory while it’s running. They are written into $HISTFILE (i.e, ~/.bash_history) when a user logs off.

```console
echo $HISTFILE           
/home/meow/.bash_history
```

This post is a cheat sheet for common methods attackers use to hide commands from being saved in the history file or in memory

## Leading Space
Might not be enabled by default in some distros

Starting each command with a leading space character

```console
echo "hello"
hello
```

```console
echo "ritsec"
ritsec
```

```console
history 
    1  ls
    2  echo "hello"
    3  history 
```
    
Notice that the command $echo "hello" was saved history unlike the commas with a leading space $ echo "ritsec". This is possible because of HISTCONTROL environment variable

```console
head -2 /etc/os-release
 NAME="Ubuntu" 
 VERSION="18.04.3 LTS (Bionic Beaver)"
```

```console
echo $HISTCONTROL
 ignoredups:ignorespace
```

## HISTFILE
The HISTFILE environment variable specifies bash history file

```console
man bash
HISTFILE
  The  name  of the file in which command history is saved (see HISTORY be‐
  low).  The default value is ~/.bash_history.  If unset, the command  his‐
  tory is not saved when a shell exits.
  the  value of HISTIGNORE.  The pattern matching honors the setting of the
  extglob shell option.
```

```console
echo $HISTFILE
/home/meow/.bash_history
To avoid recording commands to the file in $HISTFILE set HISTFILE value to /dev/null
```
```console
HISTFILE=/dev/null
```
OR
```console
export HISTFILE=/dev/null
```

## unset
```console
man bash
unset
  Remove variable or function names
```
We can use unset to remove the variable HISTFILE for the current session

```console
echo $HISTFILE
/root/.bash_history
unset HISTFILE
echo $HISTFILE
```
Note that it will only effect the current session. If you start another session the variable HISTFILE will still be set unlike changing $HISTILE value to /dev/null

## HISTSIZE & HISTFILESIZE
Notice the distinction between file: on disk - and list: in memory.

HISTSIZE is the number of lines or commands that are stored in memory in a history list while your bash session is ongoing.

```console
man bash
HISTSIZE
  The number of commands to remember in the command  history  (see  HISTORY
  below).   If  the value is 0, commands are not saved in the history list.
  Numeric values less than zero result in every command being saved on  the
  history  list  (there  is no limit).  The shell sets the default value to
  500 after reading any startup files.
```

In order to remove all commands from to the history list in memory change the size to 0

```console
echo $HISTSIZE
1000
```
```console
HISTSIZE=0  # OR export HISTSIZE=0
echo $HISTSIZE
0
HISTFILESIZE is the number of lines or commands that
```

are allowed in the history file at startup time of a session, and
are stored in the history file at the end of your bash session for use in future sessions.
```console
man bash
HISTFILESIZE
  The  maximum  number  of  lines contained in the history file.  When this
  variable is assigned a value, the history file is  truncated,  if  neces‐
  sary, to contain no more than that number of lines by removing the oldest
  entries.  The history file is also truncated to this size  after  writing
  it  when a shell exits.  If the value is 0, the history file is truncated
  to zero size.  Non-numeric values and numeric values less than  zero  in‐
  hibit truncation.  The shell sets the default value to the value of HIST‐
  SIZE after reading any startup files.
```

```console
echo $HISTFILESIZE
2000
```
```console
HISTFILESIZE=0  # OR export HISTFILESIZE=0
```

## Killing Bash Process
Using the kill command we can exit the session without saving commands in memory to disk using;

```console
kill -9 $$
```

## Using More
We can hide a command from being saved in memory using more ability to excute commands by prepending them with !
```console
!<cmd> or :!<cmd> Execute <cmd> in a subshell
```
At the more prompt type ! or :! followed by your command.

This same technique can be used with other GTFBIN(https://gtfobins.github.io/) like vim

## Clearing the History
Rather than disabling command history, we can clear the history on the current bash shell by simply using the history command with the -c (clear) flag

```console
history -c
```
Then, to make certain the changes are written to disk, we need to tell the history command to write to disk with the -w flag

```console
history -w
```
This only clears the history of the current shell. Commands run in other shells will remain on disk.

REFS
https://secbytes.net/Hiding-Your-Tracks-Bash-History/
