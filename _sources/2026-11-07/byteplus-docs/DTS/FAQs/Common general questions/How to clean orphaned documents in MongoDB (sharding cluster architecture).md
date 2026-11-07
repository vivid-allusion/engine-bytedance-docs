---
title: "How to clean orphaned documents in MongoDB (sharding cluster architecture)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/how-to-clean-orphaned-documents-in-MongoDB-sharding-cluster-architecture"
---

Orphaned documents refer to documents that exist in the database but cannot be accessed through regular queries due to broken references, missing metadata, shard inconsistencies, or documents that should have been deleted but still remain. This topic describes how to query and delete orphaned documents.

<span id="e0Pmo9zl"></span>
## Migration impact

DTS extracts full data from shard when migrating a cluster. Normal documents and orphaned documents are distributed on different shards; DTS does not distinguish between them and migrates all data to the target database. DTS uses the ignore conflict strategy for MongoDB migration, so the final document status in the target database depends on which document migrates first, potentially causing inconsistent data content or row counts.

<span id="DPQV5z1z"></span>
## Precautions


* The orphaned documents cleaning method is the same for the Document Database MongoDB edition and self\-built MongoDB.

* The command to query orphaned documents scans documents on all shard nodes and traverses the entire collection. When the document's data volume is large, query elapsed time will be longer, and it will put certain query pressure on the database instance. Therefore, it is recommended to carefully operate after evaluating the impact of data query on business.

* It is recommended to clean orphaned documents directly during business off\-peak hours.

* The cleaning operation requires connection to the Shard nodes of the cluster. For how to obtain Shard node information of the instance cluster, refer to [view connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction?lang=zh#.5p-l55yL6L-e5o6l5Zyw5Z2A).

   The cluster Shard nodes of the document database MongoDB version are not open for connection by default. If you cannot connect to the Shard node, enable ShardIP before operation, or [submit tickets](https://console.byteplus.com/workorder/create/).

* If there are multiple databases in the instance, orphaned documents in each database need to be cleaned separately.


<span id="FzTaFRgp"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following takes the document database MongoDB version instance as an example. The method for cleaning orphaned documents of a self\-built MongoDB instance is consistent with that of the document database MongoDB version instance.</div>



1. Disable the source end balancer.

   1. Connect to MongoDB instance via Mongo shell. For specific procedures, refer to [Connect to Mongo instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell?lang=zh).

   2. Execute the following command to disable the balancer.

      ```Bash
      sh.stopBalancer()
      ```
      

   3. Execute the following command to verify whether the balancer is closed successfully.

      ```Bash
      sh.getBalancerState()
      ```
      

      If the result is `false`, the balancer has been disabled successfully.

2. Pause the automatic backup function of the MongoDB instance to prevent the backup system from automatically restarting the balancer.

   The document database MongoDB version instances of Volcengine currently do not automatically restart the balancer; hence, pausing the automatic backup function of the document database MongoDB version instances is not required. Perform operations according to the actual situation.

3. Query orphaned documents

   The command to query orphaned documents scans documents on all shard nodes and traverses the entire collection. When the document's data volume is large, query elapsed time will be longer, and it will put certain query pressure on the database instance. Therefore, it is recommended to carefully operate after evaluating the impact of data query on business. Orphaned documents can be cleaned directly.

   1. Connect to MongoDB instance via Mongo shell. For specific procedures, refer to [Connect to Mongo instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell?lang=zh).

   2. Execute the following command to view orphaned documents in the target database collection. This example uses `db_name.collection_01` (read from the secondary node):

      ```Bash
      db.getSiblingDB("db_name").collection_01
        .find()                          
        .readPref("secondary")            
        .readConcern("local")             
        .explain("executionStats")       
      ```
      

      Parameter descriptions:

         * `.find()`: queries all documents in the `collection_01` collection.

         * `.readPref("secondary")`: reads from shard secondary nodes (reduces primary server pressure).

         * `.readConcern("local")`: reads the latest local data from secondary nodes (low delay).

         * `.explain("executionStats")`: returns only execution performance statistics without data.

   1. Check the `chunkSkips` attribute in the `SHARDING_FILTER` stage of the command result; this value represents the number of orphan documents in the checked collection on the current shard node. If this value is greater than zero, it indicates the presence of orphaned documents on the shard node.

   The command output example is as follows:

      This indicates that `103494661` documents (`nReturned: 103494661`) were returned during the `COLLSCAN` phase before the `SHARDING_FILTER` phase. During the `SHARDING_FILTER` phase, `10` documents (`chunkSkips: 10`) were filtered, resulting in a final return of `103494651` documents (`nReturned: 103494651`). Therefore, 10 orphan documents were detected in this example.

      ```Bash
      {
        queryPlanner: {
          mongosPlannerVersion: 1,
          winningPlan: {
            stage: 'SHARD_MERGE',
            shards: [
              {
                shardName: 'rs-mongo-shard-368c69*******-s4',
                executionSuccess: true,
                executionStages: {
                  stage: 'SHARDING_FILTER',
                  nReturned: 103494661,
                  executionTimeMillisEstimate: 48608,
                  works: 103494663,
                  advanced: 103494651,
                  needTime: 1,
                  needYield: 0,
                  saveState: 808552,
                  restoreState: 808552,
                  isEOF: 1,
                  invalidates: 0,
                  chunkSkips: 10,
                  inputStage: {
                    stage: 'COLLSCAN',
                    nReturned: 103494661,
                    executionTimeMillisEstimate: 18607,
                    works: 103494663,
                    advanced: 103494661,
                    needTime: 1,
                    needYield: 0,
                    saveState: 808552,
                    restoreState: 808552,
                    isEOF: 1,
                    invalidates: 0,
                    direction: 'forward',
                    docsExamined: 103494661
                  }
                }
              }
            ]
          }
        },
        serverInfo: {
          host: 'mongo-shard-368c69*******-0',
          port: 40000,
          version: '4.0.3-57c7d591',
          gitVersion: '57c7d591f4341da492e90c86476937d9215*******'
        },
        ok: 1,
        operationTime: Timestamp({ t: 1767773112, i: 526 }),
        '$clusterTime': {
          clusterTime: Timestamp({ t: 1767773112, i: 532 }),
          signature: {
            hash: Binary(Buffer.from("55aba0423e8f1267a599152750b38496210*******", "hex"), 0),
            keyId: Long("75535953704381*******")
          }
        }
      }
      ```
      

4. Clean orphaned documents

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there are multiple databases in the instance, orphaned documents in each database need to be cleaned separately.   </div>
   

   1. Download the following script file to an environment that can directly connect to the MongoDB Shard node. It is recommended to name the script file `cleanupOrphaned.js` for cleaning orphaned documents.

   ```JavaScript
   function cleanupOrphaned(coll) {
     var nextKey = { };
     var result;
     
     while ( nextKey != null ) {
       result = db.adminCommand( { cleanupOrphaned: coll, startingFromKey: nextKey } );
     
       if (result.ok != 1)
          print("Unable to complete at this time: failure or timeout.")
     
       printjson(result);
     
       nextKey = result.stoppedAtKey;
     }
   }
   
   var dbName = '<your_db_name>'
   db = db.getSiblingDB(dbName)
   db.getCollectionNames().forEach(function(collName) {
           cleanupOrphaned(dbName + "." + collName);
   });
   ```
   

   2. Modify parameters `var dbName` to the target database name.

   3. Execute the following command to clean orphan documents in all collections of the specified database under the Shard node.

   ```Bash
   mongosh --host <ShardIP> --port <Primaryport> --authenticationDatabase <database> -u <username> -p <password> cleanupOrphaned.js
   ```
   

   Parameter descriptions:

      * `ShardIP`: the IP address of the Shard node.

      * `Primary port`: the service port of the Primary node in the Shard node.

      * `database`: the authentication database name, which is the database to which the database account belongs.

      * `username`: the account number to log in to the database.

      * `password`: the password to log in to the database.

      The following example clears orphaned documents on shard0 node:

      ```Bash
      mongosh --host 10.129.1.112 --port 3717 --authenticationDatabase admin -u root -p '*****' cleanupOrphaned.js > shard0.txt
      ```
      

5. Enable the Balancer of the source database instance to restore automatic data balancing on the source database instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After data migration completes, enable the Balancer of the source database instance based on the following prompt.</div>



   1. Connect to MongoDB instance via Mongo shell. For specific procedures, refer to [Connect to Mongo instance via Mongo shell](https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell?lang=zh).

   2. Execute the following command to disable the balancer.

      ```Bash
      sh.startBalancer()
      ```
      

   3. execute the following command to verify if it has been enabled successfully.

      ```Bash
      sh.getBalancerState()
      ```
      

      if the return is `true`, it means balancer has been enabled successfully.

6. Enable the automatic backup function of the source database instance as needed.


<span id="2EHv8OGx"></span>
## What to do if the orphan document cleanup never completes?

If idle cursors exist on the namespace corresponding to the orphan document, the cleanup process may never complete, and the following information will appear in the mongod logs of the corresponding orphan document:

```Bash
Deletion of DATABASE.COLLECTION range [{ KEY: VALUE1 }, { KEY: VALUE2 }) will be scheduled after all possibly dependent queries finish
```


Connect to mongod via mongo shell and execute the following command to check if idle cursors exist on the current shard. if they exist, restart mongod or use the killCursors command to clear all idle cursors, then clean the orphaned documents again. for more information, refer to the [Jira ticket](https://jira.mongodb.org/browse/SERVER-50182).

```Bash
db.getSiblingDB("admin").aggregate( [{ $currentOp : { allUsers: true, idleCursors: true } },{ $match : { type: "idleCursor" } }] )
```
