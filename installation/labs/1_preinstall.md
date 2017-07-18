sudo yum install mariadb-server 


Redirecting to /bin/systemctl start  mariadb.service
[centos@ip-172-31-17-188 ~]$ sudo /usr/bin/mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y
New password:Password5
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] 

Password: Q1w2e3r4
systemctl start  mariadb.service

 vi /etc/my.cnf
Config My.cnf


#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log
server-id=2       

Server Id diferentes




GRANT REPLICATION SLAVE ON *.* TO 'root'@'ip-172-31-16-180' IDENTIFIED BY 'Password5';


Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.


#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log
server-id=1

 


MariaDB [(none)]> GRANT REPLICATION SLAVE ON *.* TO 'root'@'ip-172-31-16-180' IDENTIFIED BY 'Password5';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> SET GLOBAL binlog_format = 'ROW';
Query OK, 0 rows affected (0.01 sec)

MariaDB [(none)]> FLUSH TABLES WITH READ LOCK;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>          

MariaDB [(none)]> SHOW MASTER STATUS;
+-------------------------+----------+--------------+------------------+
| File                    | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+-------------------------+----------+--------------+------------------+
| mysql_binary_log.000001 |      245 |              |                  |
+-------------------------+----------+--------------+------------------+
1 row in set (0.00 sec)                                                                       



MariaDB [(none)]> FLUSH TABLES WITH READ LOCK;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> UNLOCK TABLES;
Query OK, 0 rows affected (0.00 sec)      


CHANGE MASTER TO MASTER_HOST='ip-172-31-25-237', MASTER_USER='root', MASTER_PASSWORD='Q1w2e3r4',MASTER_LOG_FILE='mysql_binary_log.000001', MASTER_LOG_POS='245’;

vi /etc/sysconfig/selinux

ip-172-31-25-237


CHANGE MASTER TO MASTER_HOST='ip-172-31-25-237', MASTER_USER='root', MASTER_PASSWORD='Q1w2e3r4',MASTER_LOG_FILE='mysql_binary_log.000001', MASTER_LOG_POS=245; 

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 4
Server version: 5.5.52-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>  START SLAVE;
Query OK, 0 rows affected, 1 warning (0.00 sec)

MariaDB [(none)]> SHOW SLAVE STATUS \G
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: ip-172-31-25-237
                  Master_User: root
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql_binary_log.000001
          Read_Master_Log_Pos: 245
               Relay_Log_File: mariadb-relay-bin.000003
                Relay_Log_Pos: 536
        Relay_Master_Log_File: mysql_binary_log.000001
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 245
              Relay_Log_Space: 832
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
1 row in set (0.00 sec)             



sudo yum install oracle-j2sdk1.8


vi cloudera-manager.repo 
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/ 

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/RPMS/x86_64/cloudera-manager-agent-5.11.1-1.cm5111.p0.9.el7.x86_64.rpm

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/RPMS/x86_64/cloudera-manager-daemons-5.11.1-1.cm5111.p0.9.el7.x86_64.rpm

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/RPMS/x86_64/cloudera-manager-server-5.11.1-1.cm5111.p0.9.el7.x86_64.rpm

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/RPMS/x86_64/cloudera-manager-server-db-2-5.11.1-1.cm5111.p0.9.el7.x86_64.rpm

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11/RPMS/x86_64/enterprise-debuginfo-5.11.1-1.cm5111.p0.9.el7.x86_64.rpm

 cd /usr/share/cmf/schema/
[root@ip-172-31-25-237 schema]# ls
mysql  oracle  postgresql  scm_database_functions.sh  scm_prepare_database.sh 

create database amon DEFAULT CHARACTER SET utf8;
grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'amon_password';

create database rman DEFAULT CHARACTER SET utf8;
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman_password';

create database metastore DEFAULT CHARACTER SET utf8;
grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'hive_password';

create database sentry DEFAULT CHARACTER SET utf8;
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'sentry_password';

create database nav DEFAULT CHARACTER SET utf8;
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'nav_password';

create database navms DEFAULT CHARACTER SET utf8;
grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'navms_password';

create database oozie;
grant all privileges on oozie.* to 'oozie'@'localhost' identified by 'oozie';
grant all privileges on oozie.* to 'oozie'@'%' identified by 'oozie';

create database hue default character set utf8 default collate utf8_general_ci;
grant all on hue.* to 'hue'@'%' identified by 'huepassword';
select * from information_schema.schemata;



sh scm_prepare_database.sh mysql -uroot -p scm scm scm
Enter database password:
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!   

 show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| amon               |
| metastore          |
| mysql              |
| nav                |
| navms              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+    

vi /etc/sysconfig/selinux

systemctl stop mariadb


systemctl start cloudera-scm-server


Cloudera Manager

ip-172-31-25-237.ec2.internal,ip-172-31-19-252.ec2.internal,ip-172-31-17-51.ec2.internal,ip-172-31-25-61.ec2.internal


Cloudera recommends setting /proc/sys/vm/swappiness to a maximum of 10. Current setting is 30. Use the sysctl command to change this setting at run time and edit /etc/sysctl.conf for this setting to be saved after a reboot. You can continue with installation, but Cloudera Manager might report that your hosts are unhealthy because they are swapping. The following hosts are affected: 
Transparent Huge Page Compaction is enabled and can cause significant performance problems. Run "echo never > /sys/kernel/mm/transparent_hugepage/defrag" and "echo never > /sys/kernel/mm/transparent_hugepage/enabled" to disable this, and then add the same command to an init script such as /etc/rc.local so it will be set on system reboot. The following hosts are affected: 


lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  20G  0 disk
└─xvda1 202:1    0  20G  0 part /
xvdb    202:16   0  40G  0 disk
xvdc    202:32   0  40G  0 disk  



mkfs -t ext4 /dev/xvdb
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
2621440 inodes, 10485760 blocks
524288 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2157969408
320 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

https://devopscube.com/mount-ebs-volume-ec2-instance/

mkfs -t ext4 /dev/xvdc
mkfs -t ext4 /dev/xvdb
mkdir /data/
mkdir /data/d1
mkdir /data/d2

mount /dev/xvdb /data/d1/
mount /dev/xvdc /data/d2/


#/dev/xvdb       /data/d1/   ext4    defaults,nofail 
#/dev/xvdc       /data/d2/   ext4    defaults,nofail

cp /etc/fstab /etc/fstab.bak




echo "/dev/xvdb       /data/d1/   ext4    defaults" >> /etc/fstab
echo “/dev/xvdc       /data/d2/   ext4    defaults” >> /etc/fstab




