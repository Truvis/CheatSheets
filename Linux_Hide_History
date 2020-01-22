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
