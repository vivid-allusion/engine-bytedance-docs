---
title: "Setting up PostgreSQL primary-secondary architecture"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-PostgreSQL-primary-replica-architecture"
---

PostgreSQL is a powerful, open\-source object\-relational database management system (ORDBMS). It supports NoSQL data types (such as JSON, XML, and hstore) and GIS (Geographic Information System) processing. You can use PostgreSQL in scenarios such as location\-based applications and online transaction processing.

## Software versions

* Operating system: In the example provided in this topic, CentOS 7.6 is used. You can also use CentOS 7.9, veLinux 1.0 (CentOS compatible version), or other CentOS 7 series images.

* PostgreSQL: In the example provided in this topic, PostgreSQL 11 is used.

## Prerequisites

* A Linux instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* In the security group associated with the instance, inbound TCP traffic on port 5432 is allowed.

## Step 1: Set up a primary node

1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to install PostgreSQL.

   ```Plain Text
   yum update -y
   yum -y install https://mirrors.ivolces.com/postgresql/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
   ```

3. Execute the following commands to install the client package and server package.

   ```Plain Text
   yum -y install postgresql11
   yum -y install postgresql11-server
   ```

4. Execute the following command to initialize PostgreSQL.

   ```Plain Text
   /usr/pgsql-11/bin/postgresql-11-setup initdb
   ```

5. Execute the following command to start the PostgreSQL service.

   ```Plain Text
   systemctl start postgresql-11
   ```

6. Execute the following command to specify that the PostgreSQL service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable postgresql-11
   ```

7. Execute the following command to log in with "postgres", the default account automatically generated after you install the service.

   ```Plain Text
   su - postgres
   ```

8. Execute the following command to access the PostgreSQL interactive terminal.

   ```Plain Text
   psql
   ```

9. Execute the following command to set a password for the default account "postgres" to enhance account security.

   ```Plain Text
   ALTER USER postgres WITH PASSWORD 'Password';
   ```

10. Execute the following commands to create a new database account, set its password, and grant permissions.

   ```Plain Text
   create role Username login replication encrypted password 'Password';
   ```

11. Input `\q`, and press `Enter` to exit the interactive terminal.

12. Input `exit` to exit PostgreSQL.

13. Modify the `pg_hba.conf` configuration file.

   1. Execute the following command to open the file.

      ```Plain Text
      vim /var/lib/pgsql/11/data/pg_hba.conf
      ```

   2. Press `i` key to enter edit mode, and then add the following content under `IPv4 local connections`.

      ```Plain Text
      host all all ${Secondary Node VPC IPv4 CIDR Block} md5    #Allow MD5 password authentication connections from the VPC CIDR block
      host replication  ${Username}   ${Secondary Node VPC IPv4 CIDR Block} md5  #Allow users to synchronize data from the replication database
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

14. Modify the `postgresql.conf` configuration file.

   1. Execute the following command to open the file.

      ```Plain Text
      vim /var/lib/pgsql/11/data/postgresql.conf
      ```

   2. Press `i` key to enter edit mode, and then find the following parameters and modify them. Note that you need to remove the `#` before the parameters.

      ```Plain Text
      wal_level = hot_standby  # Enable hot standby mode
      synchronous_commit = on  # Enable synchronous replication
      listen_addresses = '*'   # Listening IP address, set to *
      max_wal_senders = 32     # Maximum number of synchronous processes
      wal_sender_timeout = 60s # Timeout for data transmission by the streaming replication host
      max_connections = 500    # Maximum number of connections; the max_connections on the standby must be greater than that on the primary
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

15. Execute the following command to restart the PostgreSQL service.

   ```Plain Text
   systemctl restart postgresql-11
   ```

## Step 2: Set up a secondary node

1. Execute the following commands to install PostgreSQL.

   ```Plain Text
   yum update -y
   yum -y install https://mirrors.ivolces.com/postgresql/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
   ```

2. Execute the following commands to install the client package and server package.

   ```Plain Text
   yum -y install postgresql11
   yum -y install postgresql11-server
   ```

3. Execute the following command to specify the backup directory via the pg_basebackup tool. The password is the one for the database account.

   ```Plain Text
   pg_basebackup -h ${Primary Node VPC Address} -U ${Database Username} -D /var/lib/pgsql/11/data -X stream -P
   ```

4. Execute the following command to copy the relevant configuration files from the primary node to the recovery.conf file in the backup directory.

   ```Plain Text
   cp /usr/pgsql-11/share/recovery.conf.sample /var/lib/pgsql/11/data/recovery.conf
   ```

5. Modify the `recovery.conf` configuration file.

   1. Execute the following command to open the file.

      ```Plain Text
      vim /var/lib/pgsql/11/data/recovery.conf
      ```

   2. Press `i` key to enter edit mode, and then find the following parameters and modify them. Note that you need to remove the `#` before the parameters.

      ```Plain Text
      standby_mode = on     #Declare this node as a standby
      primary_conninfo = 'host=Primary Node VPC Address port=5432 user=Database_Username  password=Database_Password' #Corresponding connection information for the primary database
      recovery_target_timeline = 'latest' #Stream replication synchronizes to the latest data
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

6. Modify the `postgresql.conf` configuration file.

   1. Execute the following command to open the file.

      ```Plain Text
      vim /var/lib/pgsql/11/data/postgresql.conf
      ```

   2. Press `i` key to enter edit mode, and then find the following parameters and modify them. Note that you need to remove the `#` before the parameters.

      ```Plain Text
      listen_addresses= '*'              # Listening internal IP address, set to *
      max_connections = 600              # Maximum number of connections; the max_connections on the standby must be greater than that on the primary
      hot_standby = on                   # Enable hot standby
      max_standby_streaming_delay = 30s  # Maximum delay time for data stream backup
      wal_receiver_status_interval = 1s # Maximum interval for the standby node to report its status to the primary node
      hot_standby_feedback = on          # If there is erroneous data replication, provide feedback to the primary
      ```

   3. Press `Esc`, enter `:wq`, and then press Enter to save the modifications and close the file.

7. Execute the following command to modify the group and owner of the data directory.

   ```Plain Text
   chown -R postgres.postgres /var/lib/pgsql/11/data
   ```

8. Execute the following command to start the PostgreSQL service.

   ```Plain Text
   systemctl start postgresql-11
   ```

9. Execute the following command to specify that the PostgreSQL service automatically starts upon instance startup.

   ```Plain Text
   systemctl enable postgresql-11
   ```

## Step 3: Verify whether the setup is completed

1. Log in to the primary node and execute the following command to view the sender process.

   ```Plain Text
   ps aux |grep sender
   ```

   If the following output is displayed, the primary node is set up successfully.

   ```Plain Text
   postgres 17281  0.0  0.0 416252  3644 ?        Ss   15:31   0:00 postgres: walsender wxt 192.168.0.127(38924) streaming 0/3000140
   root     17291  0.0  0.0 112812   980 pts/0    S+   15:31   0:00 grep --color=auto sender
   ```

2. Log in to the secondary node and execute the following command to view the receiver process.

   ```Plain Text
   ps aux |grep receiver
   ```

   If the following output is displayed, the secondary node is set up successfully.

   ```Plain Text
   postgres 16930  0.0  0.0 422320  3668 ?        Ss   15:31   0:00 postgres: walreceiver   streaming 0/3000140
   root     16942  0.0  0.0 112812   976 pts/0    S+   15:31   0:00 grep --color=auto receiver
   ```

3. Log in to the primary node and execute the following command on the primary database to check the secondary database status.

   1. Execute the following command to log in to "postgres", the default account automatically generated after you install the service.

      ```Plain Text
      su - postgres
      ```

   2. Execute the following command to access the PostgreSQL interactive terminal.

      ```Plain Text
      psql
      ```

   3. Execute the following command to check the secondary database status.

      ```Plain Text
      select * from pg_stat_replication;
      ```

      The following output is displayed.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48051f4e80a0f29a90fdae9149d38e55.png)

4. Create a new database on the primary database and verify whether the secondary database automatically synchronizes it.

   1. Execute the following command to create a new primary database.

      ```Plain Text
      create database testdb;
      ```

   2. Log in to the secondary node, access the PostgreSQL interactive terminal, and execute the following command to view the secondary database.

      ```Plain Text
      \l
      ```

      If the following output is displayed, the secondary database has synchronized successfully.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/7da81fd48efb4dd0ac13a53d7ae17a5c.png)
