---
title: "Restoring replica set instance data to self-built database via physical backup"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/restor-self-managed-db-from-physical-backup-file"
---

Document database MongoDB edition supports backup file download. You can download backup files locally and restore data to a local self\-hosted MongoDB database using these files for offline analysis or performance testing.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Install the corresponding version of MongoDB locally or on an ECS server. For installation methods, see the [MongoDB start guide](https://docs.mongodb.com/guides/server/install/).

   This article uses the installation of MongoDB version 4.0 on a [Cloud Server ECS instance](https://console.byteplus.com/ecs/instance) as an example.

* Create the directory for the database on the server with MongoDB installed to perform physical recovery operations.

   This article uses `/root/mongotest` as the directory for the physical recovery operation database.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The locally built MongoDB database (hereinafter referred to as "self\-built MongoDB") must maintain the same database version as the document database MongoDB edition (hereinafter referred to as "MongoDB"). For example, MongoDB uses database version 4.0, and a self\-hosted MongoDB must also use version 4.0.

* MongoDB supports two instance architectures: replica sets and sharded clusters. In a replica set instance, there is only one copy of the data, while in a sharded cluster, each shard holds a copy of the data. You can choose which data to restore based on your business needs.

* It is not recommended to restore data to a self\-built MongoDB sharded cluster because self\-built clusters lack physical backup routing. Therefore, even if you restore each shard's data to every shard in the self\-built cluster, Mongos can only read data from the primary shard.


<span id=".5q2l6aqk5LiA77ya5LiL6L295Y-K6Kej5Y6L54mp55CG5aSH5Lu95paH5Lu2"></span>
## Step 1: Download and extract the physical backup file


1. On the ECS with MongoDB service installed, download the physical backup file of the target MongoDB instance using the following command.

   ```Bash
   wget -c '<public download URL of the backup file>' -O <custom filename>.zip
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MongoDB supports generating data backups and log backups through physical backup methods. Use the <strong>data backup</strong> for restoration. You can manually create a physical backup in the MongoDB console. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/mongodb/manual-backup">Manual backup</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can find the public download URL of the physical backup file in the MongoDB console. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/mongodb/manage-backup-file#OQemzRNR">Downloading backup files</a>.   </div>
   

2. Run the following command to extract the physical backup file.

   ```Bash
   unzip <custom_filename>.zip
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After extraction, you will see a <code>metadata</code> file and a <code>data</code> folder in the current directory (physical backup files for sharded clusters also include a <code>mongo</code> folder containing each shard's backup data). Use the physical backup data under the <code>/data/physic/</code> folder in the following steps. The backup data filename is <code>full-xxx</code> (for example, <code>full-168857646998639****</code>).   </div>
   

3. Run the following command to create a `data` directory in `/root/mongotest` and move the extracted MongoDB physical backup files to the `/root/mongotest/data/` directory.

   ```Bash
   mkdir -p /root/mongotest/data && mv <physical backup file> /root/mongotest/data
   ```
   

   Example is as follows.

   ```Bash
   mkdir -p /root/mongotest/data && mv /root/data/physic/full-168857646998639**** /root/mongotest/data
   ```
   


<span id=".5q2l6aqk5LqM77ya5bCG54mp55CG5aSH5Lu95pWw5o2u5oGi5aSN6Iez6Ieq5bu6LW1vbmdvZGI="></span>
## Step 2: Restore the physical backup data to the self\-built MongoDB


1. Run the following command to create a configuration file `mongod.conf` in the `/root/mongotest` folder.

   ```Bash
   touch /root/mongotest/mongod.conf
   ```
   

2. Enter vi `/root/mongotest/mongod.conf` in the command line to open the `mongod.conf` file, then press `i` on the keyboard to enable edit mode.

3. Modify the file paths in the following configuration to your actual directories, then copy them into the `mongod.conf` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This operation uses restoring to a single\-node mode self\-built MongoDB database as an example; therefore, the startup mode in the configuration file below is single\-node mode with authentication disabled.   </div>
   

   ```Yaml
   systemLog:
     destination: file
     path: <current node's MongoDB log file path>
     logAppend: true
   storage:
     dbPath: <current node's MongoDB data file path>
   net:
     bindIp: 127.0.0.1
     port:  27011
   storage:
      journal:
         enabled: true
   processManagement:
     fork: true
     pidFilePath: <current node's MongoDB PID file (the process ID file) path>
   ```
   

   The configuration file example is as follows.

   ```Yaml
   systemLog:
     destination: file
     path:  /root/mongotest/mongod.conf
     logAppend: true
   storage:
     dbPath: /root/mongotest/data/  
   net:
     bindIp: 127.0.0.1
     port:  27011
   storage:
      journal:
         enabled: true
   processManagement:
     fork: true
     pidFilePath: /root/mongotest/mongodb.pid
   ```
   

4. Press Esc to exit edit mode, then type `:wq` to save and exit.

5. Navigate to the `bin` directory of the MongoDB installation package, then run the following command to start MongoDB using the newly created configuration file `mongod.conf`.

   ```Bash
   ./mongod --config <path to mongod.conf file>
   ```
   

   Example is as follows.

   ```Bash
   ./mongod --config /root/mongotest/mongod.conf
   ```
   

6. After MongoDB starts, run the following command to connect to the self\-hosted MongoDB database via the Mongo Shell tool.

   ```Bash
   ./mongo --port 27011
   ```
   

7. Once connected, you can run the `show dbs` command in the Mongo Shell tool to list all databases in the local MongoDB and verify if the restoration succeeded.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After confirming successful restoration, run the <code>exit</code> command in Mongo Shell to quit.   </div>
