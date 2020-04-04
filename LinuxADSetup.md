
# Add Linux machines to ADDS

## Debian
apt-get realmd

## CentOS
yum install sssd realmd oddjob oddjob-mkhomedir adcli samba-common samba-common-tools krb5-workstation openldap-clients policycoreutils-python -y


realm join domain.tld --user=username

