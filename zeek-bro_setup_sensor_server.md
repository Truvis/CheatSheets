This was done using CentOS 8 base install. 

# CentOS 8
### ENABLE “NETWORK” SERVICE AND DISABLE NIC OFFLOADING FUNCTIONS & SET SNIFFING NETWORK INTERFACES TO PROMISCUOUS MODE
```
yum install network-scripts
ethtool -g enp2s0
vim /etc/sysconfig/network-scripts/ifcfg-<sniffinginterface> 
 >>> ETHTOOL_OPTS="-G ${DEVICE} rx <max ring parameter determined from step 1 above>; -K ${DEVICE} rx off; -K ${DEVICE} tx off; -K ${DEVICE} sg off; -K ${DEVICE} tso off; -K ${DEVICE} ufo off; -K ${DEVICE} gso off; -K ${DEVICE} gro off; -K ${DEVICE} lro off"
systemctl enable network
systemctl restart network
vim etc/systemd/system/promisc.service
>>> [Unit]
>>> Description=Makes an interface run in promiscuous mode at boot
>>> After=network.target
>>> [Service]
>>> Type=oneshot
>>> ExecStart=/usr/sbin/ip link set dev enp2s0 promisc on
>>> TimeoutStartSec=0
>>> RemainAfterExit=yes
>>> [Install]
>>> WantedBy=default.target
chmod u+x /etc/systemd/system/promisc.service
systemctl start promisc.service
systemctl enable promisc.service\
ip a show enp2s0 | grep -i promisc
```
## INSTALL ZEEK DEPENDENCIES GEO IP UPDATE
- As root/sudo, edit /etc/yum.repos.d/CentOS-PowerTools.repo and set the “enabled” field to 1, to add the PowerTools repositor
```
yum --enablerepo=extras install epel-release
yum install cmake make gcc gcc-c++ flex bison jemalloc-devel libpcap-devel openssl-devel platform-python-devel swig zlib-devel
yum update
yum install libmaxminddb-devel
```
- Create MaxMind Account and then download and extract the GeoIP Database to  /usr/share/GeoIP/GeoLite2-City.mmdb

## CREATE THE ZEEK USER AND DIRECTORY TO INSTALL/RUN
```
groupadd zeek
useradd zeek -g zeek
passwd zeek
mkdir /opt/zeek
chown -R zeek:zeek /opt/zeek
chmod 750 /opt/zeek
```

## DOWNLOAD, COMPILE, AND INSTALL ZEEK
(compile time will take awhile)
```
su zeek
cd
wget https://download.zeek.org/zeek-3.2.2.tar.gz
tar -xzvf zeek-3.2.2.tar.gz
cd zeek-3.2.2
./configure --prefix=/opt/zeek --enable-jemalloc
make
make install
exit
setcap cap_net_raw=eip /opt/zeek/bin/zeek
setcap cap_net_raw=eip /opt/zeek/bin/capstats
pathmunge /opt/zeek/bin (REF: https://serverfault.com/questions/102932/adding-a-directory-to-path-in-centos)
```
- Edit /opt/zeek/etc/node.cfg and wipe the file to use this:
```
[logger]
type=logger
host=localhost

[manager]
type=manager
host=localhost

[proxy-1]
type=proxy
host=localhost

[worker-1]
type=worker
host=localhost
interface={int}

[worker-2]
type=worker
host=localhost
interface={int}

[worker-3]
type=worker
host=localhost
interface={int}

[worker-4]
type=worker
host=localhost
interface={int}
```
- Run
```
zeekctl deploy
zeekctl status
crontab -e
>>> */5 * * * * /opt/zeek/bin/zeekctl cron
```


