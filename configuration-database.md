# Configuration Database.


| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| export ORACLE_BASE=/u01/app/oracle                            |                                                                            |
| export ORACLE_HOME=/u01/app/oracle/product/12.2.0/dbhome_1    |                                                                            |
| export ORACLE_SID=exampleSID                                  |                                                                            |
| export PATH=$ORACLE_HOME/bin:$PATH                            |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| echo $ORACLE_BASE                                             |                                                                            |
| echo $ORACLE_HOME                                             |                                                                            |
| echo $ORACLE_SID                                              |                                                                            |
| echo $PATH                                                    |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
|                                                               |                                                                            |

`env | grep ORACLE_HOME`
`env | grep ORACLE_SID`
`env | grep -i oracle`
`env | grep -i ora | sort`





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| . oraenv                                                      |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| find -name tnsnames.ora                                       |                                                                            |
| find -name listener.ora                                       |                                                                            |
| hostname                                                      |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| lsnrctl stop                                                  |                                                                            |
| lsnrctl start                                                 |                                                                            |
| lsnrctl reload                                                |                                                                            |
| lsnrctl status                                                |                                                                            |
| show parameter local_listener                                 |                                                                            |
|                                                               |                                                                            |

`ALTER SYSTEM SET LOCAL_LISTENER="/u01/app/oracle/product/12.2.0/dbhome_1/network/admin/listener.ora";`
`/u01/app/oracle/product/12.2.0/dbhome_1/network/admin`





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| sqlplus / as sysdba                                           |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| show con_name;                                                |                                                                            |
| shutdown abort;                                               |                                                                            |
| shutdown immediate;                                           |                                                                            |
| startup;                                                      |                                                                            |
| select name from V$database;                                  |                                                                            |
| select * from V$database;                                     |                                                                            |
| alter database mount;                                         |                                                                            |
| alter database open;                                          |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| select name from v$datafile;                                  |                                                                            |
| select name from v$controlfile;                               |                                                                            |
| select member from v$logfile;                                 |                                                                            |
|                                                               |                                                                            |





| Key/Command                                                   | Description                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| ps -ef|grep pmon                                              |                                                                            |
|                                                               |                                                                            |






show parameter control

============================================================= 
select * from global_name;

==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
============================================================= Tablespace
select * from V$TABLESPACE;
select name from V$TABLESPACE;

CREATE SMALLFILE TABLESPACE USR_MS DATAFILE '/u01/app/oracle/oradata/LIBPROD/USR_MS_DBFILE1.DBF' SIZE 104857600 DEFAULT NOCOMPRESS ONLINE SEGMENT SPACE MANAGEMENT AUTO;

CREATE SMALLFILE TABLESPACE LIB_MS DATAFILE '/u01/app/oracle/oradata/LIBPROD/LIB_MS_DBFILE1.DBF' SIZE 104857600 DEFAULT NOCOMPRESS ONLINE SEGMENT SPACE MANAGEMENT AUTO;

CREATE SMALLFILE TABLESPACE USR_MS DATAFILE '/u01/app/oracle/oradata/LIBTEST/USR_MS_DBFILE1.DBF' SIZE 104857600 DEFAULT NOCOMPRESS ONLINE SEGMENT SPACE MANAGEMENT AUTO;

CREATE SMALLFILE TABLESPACE LIB_MS DATAFILE '/u01/app/oracle/oradata/LIBTEST/LIB_MS_DBFILE1.DBF' SIZE 104857600 DEFAULT NOCOMPRESS ONLINE SEGMENT SPACE MANAGEMENT AUTO;



==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
============================================================= User
show user;

conn / as sysdba
conn exampleUserName/exampleUserPassword

SELECT * FROM all_users;
SELECT username FROM all_users;

SELECT * FROM dba_users;
SELECT username FROM dba_users;
SELECT * FROM dba_users WHERE username='exampleUserName';
	
SELECT * FROM user_users;
SELECT username FROM user_users;

SELECT * FROM DBA_SYS_PRIVS;
SELECT * FROM USER_ROLE_PRIVS WHERE USERNAME='exampleUserName';
SELECT * FROM USER_TAB_PRIVS WHERE Grantee = 'exampleUserName';
SELECT * FROM USER_SYS_PRIVS WHERE USERNAME = 'exampleUserName';

SELECT * FROM all_users WHERE username='exampleUserName';

SELECT * FROM session_privs;

GRANT CONNECT TO "exampleUserName";

============================================================= Script creation user USR_MS in DB libprod.
show user;
show con_name;

CREATE USER "USR_MS" IDENTIFIED BY "exampleUserPassword" DEFAULT TABLESPACE "USR_MS" TEMPORARY TABLESPACE "TEMP";
ALTER USER USR_MS QUOTA UNLIMITED on USR_MS;
GRANT CREATE SESSION TO "USR_MS";
GRANT RESOURCE TO "USR_MS";
SELECT username, account_status, default_tablespace, temporary_tablespace FROM dba_users WHERE username='USR_MS';
SELECT * FROM dba_role_privs WHERE grantee='USR_MS';
conn USR_MS/exampleUserPassword
SELECT * FROM session_privs;

============================================================= Script creation user LIB_MS in DB libprod.
show user;
show con_name;

CREATE USER "LIB_MS" IDENTIFIED BY "exampleUserPassword" DEFAULT TABLESPACE "LIB_MS" TEMPORARY TABLESPACE "TEMP";
ALTER USER LIB_MS QUOTA UNLIMITED on LIB_MS;
GRANT CREATE SESSION TO "LIB_MS";
GRANT RESOURCE TO "LIB_MS";
SELECT username, account_status, default_tablespace, temporary_tablespace FROM dba_users WHERE username='LIB_MS';
SELECT * FROM dba_role_privs WHERE grantee='LIB_MS';
conn LIB_MS/exampleUserPassword
SELECT * FROM session_privs;

============================================================= Script creation user USR_MS in DB libtest.
show user;
show con_name;

CREATE USER "USR_MS" IDENTIFIED BY "exampleUserPassword" DEFAULT TABLESPACE "USR_MS" TEMPORARY TABLESPACE "TEMP";
ALTER USER USR_MS QUOTA UNLIMITED on USR_MS;
GRANT CREATE SESSION TO "USR_MS";
GRANT RESOURCE TO "USR_MS";
SELECT username, account_status, default_tablespace, temporary_tablespace FROM dba_users WHERE username='USR_MS';
SELECT * FROM dba_role_privs WHERE grantee='USR_MS';
conn USR_MS/exampleUserPassword
SELECT * FROM session_privs;

============================================================= Script creation user LIB_MS in DB libtest.
show user;
show con_name;

CREATE USER "LIB_MS" IDENTIFIED BY "exampleUserPassword" DEFAULT TABLESPACE "LIB_MS" TEMPORARY TABLESPACE "TEMP";
ALTER USER LIB_MS QUOTA UNLIMITED on LIB_MS;
GRANT CREATE SESSION TO "LIB_MS";
GRANT RESOURCE TO "LIB_MS";
SELECT username, account_status, default_tablespace, temporary_tablespace FROM dba_users WHERE username='LIB_MS';
SELECT * FROM dba_role_privs WHERE grantee='LIB_MS';
conn LIB_MS/exampleUserPassword
SELECT * FROM session_privs;

==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
=============================================================
SQL> show pdbs
SQL> show conn_name;
SQL> select DBMS_XDB_CONFIG.gethttpport from dual;
SQL> EXEC DBMS_XDB_CONFIG.sethttpport(5500);

============================================================= Pre configuration Enterprise Manager
SQL> alter system set memory_target=3G scope=spfile;
SQL> alter system set sga_target=2G scope=spfile;
SQL> alter system set pga_aggregate_target=1G scope=spfile;
SQL> alter system set shared_pool_size=600M scope=spfile;
SQL> alter system set processes=300 scope=spfile;
SQL> alter system set session_cached_cursors=200 scope=spfile;
SQL> alter system set job_queue_processes=20 scope=spfile;
SQL> alter system set open_cursors=300 scope=spfile;

Remove this configuration or installer EM.
-mx512m -XX:MaxPermSize=512M

=============================================================
alter system register;

=============================================================
startup nomount pfile='/u01/app/oracle/product/12.2.0/dbhome_1/dbs/OEBD.ora'
startup mount pfile='/u01/app/oracle/product/12.2.0/dbhome_1/dbs/OEBD.ora'

==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
emctl status dbconsole

emca -deconfig dbcontrol db -repos drop -SYS_PWD oracle -SYSMAN_PWD oracle
emca -deconfig dbcontrol db -repos drop -SYS_PWD oracle_4U -SYSMAN_PWD oracle_4U

==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
SELECT * FROM v$version

mvn install:install-file -Dfile=path/to/your/ojdbc7.jar -DgroupId=com.oracle -DartifactId=ojdbc7 -Dversion=12.2.0.1 -Dpackaging=jar

==============================================================================================================================
==============================================================================================================================
==============================================================================================================================
