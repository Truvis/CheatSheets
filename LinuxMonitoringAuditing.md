# History

Add to .bashrc to instantly dump commands including ones with spaces. Allows for better audit and security

- PROMPT_COMMAND='history -a'
- export HISTCONTROL=

# Syslog

## LogRotate
/etc/logrotate.conf
Set how often logs are kept and when to rotate them
rotate 0 -- keep all the logs


## rsyslog vs syslog
rsyslog -- allows logging to remote and local

### /etc/rsyslog.conf 
syslog does not check or validate - use firewall for whitelisting.

service.message type {info, warning, alert...}

# journalD

stores logs as a binary -- they cant be modified

# bashrc
AuditD is better but this is a quick drop in way to monitor history with more details. Add to the .bashrc file and create a master one under /etc/profile.d

```
PROMPT_COMMAND='history -a'
export HISTCONTROL=
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
    PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND ; }"'echo -e $$\\t$USER\\t$SSH_CONNECTION\\t$HOSTNAME\\tscreen $WINDOW\\t`date +%D%t%T%t%Y%t%s`\\t$PWD"$(history 1)" >> ~/.bash_eternal_history'
    [ "$PS1" = "\\s-\\v\\\$ " ] && PS1="[\u \w]\\$ "
    if [ "x$SHLVL" != "x1" ]; then # We're not a login shell
        for i in /etc/profile.d/*.sh; do
      if [ -r "$i" ]; then
          . $i
      fi
  done
    fi
shopt -s histappend
```






