
//mysql/my.conf
[mysqld]
# Unix socket settings (making localhost work)
user            = mysql
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock

# TCP Socket settings (making 127.0.0.1 work)
port            = 3306
bind-address    = 127.0.0.1

important for loadbalancing
https://www.nginx.com/blog/mysql-high-availability-with-nginx-plus-and-galera-cluster/



MySQL 5.7 Reference Manual
https://docs.oracle.com/cd/E17952_01/mysql-5.7-en/index.html

Including MySQL NDB Cluster 7.5 and NDB Cluster 7.6


https://www.youtube.com/watch?v=64jtbkuPtvc

https://stackoverflow.com/questions/31693400/mysql-5-6-missing-ndbcluster-engine


https://www.digitalocean.com/community/tutorials/how-to-create-a-multi-node-mysql-cluster-on-ubuntu-18-04#step-2-%E2%80%94-installing-and-configuring-the-data-nodes
https://www.howtoforge.com/tutorial/how-to-install-a-mysql-cluster-on-ubuntu-16-04/
http://download.nust.na/pub6/mysql/tech-resources/articles/mysql-cluster-for-two-servers.html


followed

https://www.howtoforge.com/tutorial/how-to-install-a-mysql-cluster-on-ubuntu-16-04/

https://www.howtoforge.com/tutorial/how-to-install-a-mysql-cluster-on-ubuntu-16-04/

node js
https://www.toptal.com/mysql/mysql-master-slave-replication-tutorial

ngnix -s stop
start /b ngnix



34485
mysql:- 
UPDATE mysql.db SET Host='%' WHERE Host='localhost' AND User='username';
UPDATE mysql.user SET Host='%' WHERE Host='localhost' AND User='username';
FLUSH PRIVILEGES;

cluster:- 
ndb_mgm -e "All Report memoryusage"
ndb_mgm -e "ALL STATUS"
ndb_mgm -e "2 [start | RESTART]"
ndb_mgm -e "START BACKUP"

restart overwirting cache files, the following options can be used 
on command line
ndbd --initial
ndbd --skip-config-cache
or removing cache files with:
   rm -f /usr/mysql-cluster/*
   
   
   
ndb-connectstring: Data Nodes & SQL Nodes   
connect-string: Data Node only;
connectstring: SQL Node only






=---------------------------------------------------------------
sudo apt-get clean
sudo apt-get purge mysql*
sudo apt-get update
sudo apt-get install -f
sudo apt-get install mysql-server-5.7
sudo apt-get dist-upgrade


sudo systemctl daemon-reload
sudo systemctl enable ndb_mgmd
sudo systemctl start ndb_mgmd
sudo systemctl status ndb_mgmd

ndb_mgm>show

netstat -nltp(check port)
ps -ef | grep mysql


slave
sudo systemctl daemon-reload
sudo systemctl enable ndbd


sudo systemctl start ndbd
sudo systemctl status ndbd


mysql command to check

SHOW ENGINE NDB STATUS \G

show global status like 'ndb_number_of%';

	
------------------------------------------------------------------------------------------JenKINS--------------------------------------------------

http://15.34.81.253:8086/

sudo service jenkins restart
change port here /etc/default/jenkins





Installation



wget http://dev.mysql.com/get/Downloads/MySQL-Cluster-7.4/mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz



tar -xzvf mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz
mv mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64/ mysql/
cd ~/mysql/
cp bin/ndb_mgm* /usr/local/bin/
chmod +x /usr/local/bin/ndb_mgm*
mkdir -p /var/lib/mysql-cluster/
vim /var/lib/mysql-cluster/config.ini
---------------------------------------------------------------------------------------
[ndbd default]
NoOfReplicas=2
DataMemory=80M
IndexMemory=18M
 
[mysqld default]
 
[ndb_mgmd default]
 
[tcp default]
 
# Cluster Control / Management node
[ndb_mgmd]
hostname=192.168.1.11
 
# Data Node 1
[ndbd]
hostname=192.168.1.12
DataDir= /var/lib/mysql-cluster
 
# Data Node 1
[ndbd]
HostName=192.168.1.13
DataDir=/var/lib/mysql-cluster
 
# SQL Node
[mysqld]
hostname=192.168.1.14
 
# If you to add new SQL Node
[mysqld]



-----------------------------------------------------------------------------------

ndb_mgmd -f /var/lib/mysql-cluster/config.ini --configdir=/var/lib/mysql-cluster/

echo 'ndb_mgmd -f /var/lib/mysql-cluster/config.ini --configdir=/var/lib/mysql-cluster/' >> /etc/rc.local

netstat -plntu 
ndb_mgm
show


Data Node


apt-get install libaio1
groupadd mysql
useradd -g mysql mysql


wget http://dev.mysql.com/get/Downloads/MySQL-Cluster-7.4/mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz
tar -xzvf mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz
mv mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64/ mysql/
mv mysql /usr/local/
cd /usr/local/mysql/
./scripts/mysql_install_db --user=mysql
cp support-files/mysql.server /etc/init.d/mysql
systemctl enable mysql
mv bin/* /usr/local/bin/
rm -rf bin/
ln -s /usr/local/bin /usr/local/mysql/
chown -R root:mysql .
chown -R mysql data
vim /etc/my.cnf

-----------------------------------------------------------------
# MySQL Config
[mysqld]
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
user=mysql
 
# Run ndb storage engine
ndbcluster
# IP address management node
ndb-connectstring=192.168.1.11
 
[mysql_cluster]
# IP address management node
ndb-connectstring=192.168.1.11
 
# MySQL Pid and Log
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
--------------------------------------------------------------------


mkdir -p /var/lib/mysql-cluster/
chown -R mysql /var/lib/mysql-cluster
ndbd --initial
systemctl start mysql
mysql_secure_installation
mysql -u root -p

SQL Node

apt-get install libaio1
groupadd mysql
useradd -g mysql mysql

wget http://dev.mysql.com/get/Downloads/MySQL-Cluster-7.4/mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz
tar -xzvf mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64.tar.gz
mv mysql-cluster-gpl-7.4.27-linux-glibc2.12-x86_64/ mysql/
mv mysql /usr/local/
cd /usr/local/mysql/

./scripts/mysql_install_db --user=mysql
cp support-files/mysql.server /etc/init.d/mysql
systemctl enable mysql
mv bin/* /usr/local/bin/
rm -rf bin/
ln -s /usr/local/bin /usr/local/mysql/
chown -R root:mysql .
chown -R mysql data
vim /etc/my.cnf


-----------------------------------------------------

# MySQL Config
[mysqld]
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
user=mysql
# add line to default engine 
default-storage-engine=ndbcluster
# Run ndb storage engine
ndbcluster
# IP address management node
ndb-connectstring=192.168.1.11
 
[mysql_cluster]
# IP address management node
ndb-connectstring=192.168.1.11
 
# MySQL Pid and Log
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid


systemctl start mysql
mysql_secure_installation
--------------------------------------------------------












