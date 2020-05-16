----------------------master-----------------------------------------------------------------
[ndbd default]
noofreplicas=2

[ndbd]
hostname=192.168.0.3
id=1

[ndbd]
hostname=192.168.0.4
id=2

[ndb_mgmd]
id = 101
hostname=192.168.0.3

[ndb_mgmd]
id = 102
hostname=192.168.0.4

[mysqld]
id=51
hostname=192.168.0.3

[mysqld]
id=52
hostname=192.168.0.4

----------------------------master-----------------------------------------------------------------
[mysqld]
ndb-nodeid=51
ndbcluster
datadir=/home/billy/mysql/7_0_6/data
basedir=/home/billy/mysql/7_0_6
port=3306
server-id=51
log-bin
----------------------------------------------------------------------------------------------
[mysqld]
ndb-nodeid=52
ndbcluster
datadir=/home/billy/mysql/7_0_6/data
basedir=/home/billy/mysql/7_0_6
port=3306
server-id=52
log-bin
--------------------------------------------------

digital Badge
59466339