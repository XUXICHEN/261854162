
## 1.Fixing MySQL replication after slaves’s relay log was corrupted
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

## 2. remove all rows from table
  truncate table ***
