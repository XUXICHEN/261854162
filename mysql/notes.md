
### 1.Fixing MySQL replication after slaves’s relay log was corrupted
  Refer to page http://www.redips.net/mysql/replication-slave-relay-log-corrupted/
  
  run show slave status to get Relay_Master_Log_File and Exec_Master_Log_Pos,
  Relay_Master_Log_File: mysql-bin.002045
  Exec_Master_Log_Pos: 103641119
  
  # stop slave
  mysql> stop slave;
   
  # make slave forget its replication position in the master's binary log
  mysql> reset slave;
   
  # change slave to start reading from stopped position
  mysql> change master to master_log_file='mysql-bin.002045', master_log_pos=103641119;
   
  # start slave
  mysql> start slave;
  
  can also get the positon from /var/log/mysql/error.log  

### 2. remove all rows from table
  `truncate table ***`
  
  **to reclaim disk space**
  ```
  Currently, you cannot remove a data file from the tablespace. To decrease the size of your tablespace, use this procedure:

  Use mysqldump to dump all your InnoDB tables.
  Stop the server.
  Remove all the existing tablespace files, including the ibdata and ib_log files. If you want to keep a backup copy of the information, then copy all the ib* files to another location before the removing the files in your MySQL installation.
  Remove any .frm files for InnoDB tables.
  Configure a new tablespace.
  Restart the server.
  Import the dump files.
  ```
  
