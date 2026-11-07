---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/flink_faqs"
---

<span id="q1-the-yarn-application-application-xxxxxx-doesn-t-run-anymore"></span>
## Q1. The Yarn application application_xxxxxx doesn't run anymore.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ca97f85e4a2590158019f77e6c05303.png) </span>

When running in standalone cluster mode or yarn session mode, you may encounter scenarios where the Yarn application does not exist. The main reason is that the application task from the previous Yarn session has already ended, but the Application ID is still retained in the local `/tmp/.yarn-properties-root` file. When the SQL client does not specify `execution.target` by default, it reads the Application ID from this file and attempts to submit tasks to that Application.

**Solution:** 

Manually delete or modify the `/tmp/.yarn-properties-root` file.

<span id="q2-cloud-not-find-any-factory-for-identifier-hive-that-implements-org-apache-flink-table-planner-delegation-parserfactory-in-the-classpath"></span>
## Q2. Cloud not find any factory for identifier 'hive' that implements 'org.apache.flink.table.planner.delegation.ParserFactory' in the classpath.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e626d26625c453f4ec733978e865e08.png) </span>

When using the Hive dialect after Flink 1.16, you may encounter the above error, which is mainly caused by dependency Jar package configuration issues.

**Solution:** 

Refer to [Flink SQL Client reference—Hive Dialect table creation](https://docs.byteplus.com/docs/E-MapReduce/109229#_2-1-flink-sql-%E9%9B%86%E6%88%90-hive-connector) or [the official guide](https://docs.byteplus.com/docs/E-MapReduce/109227#use-hive-dialect).

<span id="q3-java-lang-classnotfoundexception-org-apache-ranger-authorization-hive-authorizer-rangerhiveauthorizerfactory"></span>
## Q3. java.lang.ClassNotFoundException: org.apache.ranger.authorization.hive.authorizer.RangerHiveAuthorizerFactory

When Flink uses Hive dialect mode, and the EMR cluster has enabled the ranger\-hive\-plugin and directly uses `/etc/emr/hive/conf` as the Hive configuration to create the Hive Catalog, the Flink runtime environment lacks the relevant dependencies for ranger\-hive\-plugin.

**Solution:** 


* To enable ranger\-hive\-plugin for permission verification, add ranger\-hive\-plugin to the Flink classpath, for example `ln -s /usr/lib/emr/current/ranger-hive-plugin/lib/ranger-hive-plugin-shim-2.1.1-SNAPSHOT.jar ranger-hive-plugin-shim-2.1.1-SNAPSHOT.jar`

* To disable ranger\-hive\-plugin, copy `hive-site.xml`, remove the ranger\-related configuration parameters, and use the new `hive-site.xml` to create the Hive Catalog.


<span id="q4-java-lang-unsupportedoperationexception-tos-streams-are-not-syncable-see-hadoop-17597"></span>
## Q4. java.lang.UnsupportedOperationException: tos streams are not Syncable. See HADOOP\-17597.

When writing data to TOS based on the TOS protocol, you may encounter this type of error. Additional HDFS parameters need to be added. For details about the issue, refer to [Hadoop-17597](https://issues.apache.org/jira/browse/HADOOP-17597).

**Solution:** 

Add the following parameters to the `core-site.xml` file, or add them via the EMR UI.

```bash
<property>
    <name>fs.tos.downgrade.syncable.exceptions</name>
    <value>true</value>
</property>
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9c881aee9d9383e4635c2d9e3a97450.png) </span>

<span id="q5-java-lang-verifyerror-stack-map-does-not-match-the-one-at-exception-handler-20-exception-details-location-org-apache-iceberg-hive-hivecatalog-alterhivedatabase-lorg-apache-iceberg-catalog-namespace-lorg-apache-hadoop-hive-metastore-api-database-v"></span>
## **Q5. java.lang.VerifyError: Stack map does not match the one at exception handler 20 Exception Details: Location: org/apache/iceberg/hive/HiveCatalog.alterHiveDataBase(Lorg/apache/iceberg/catalog/Namespace;Lorg/apache/hadoop/hive/metastore/api/Database;)V**

Currently, when both Hudi and Iceberg services are installed, you may encounter the above error when creating an Iceberg Hive Catalog, mainly due to conflicts between Iceberg and Hudi.

**Solution:** 


* Method 1: When installing services, install only one of Iceberg or Hudi.

* Method 2: When using Iceberg, execute the command `unlink /usr/lib/emr/current/flink/lib/hudi-flink-bundle_2.12.jar` to manually remove the Hudi\-flink dependency package.


<span id="a18276d1"></span>
## Q6: How to view the logs of running Flink jobs?

For Flink jobs running on YARN, you can view logs in the following ways:


1. YARN ResourceManager web interface:

   * Open the YARN ResourceManager web interface.

   * Find the Application ID corresponding to your Flink jobs in the interface.

   * Click this Application ID to enter the Application details page.

   * On the details page, find the "Attempt ID" with the start time closest to the current time.

   * Click this Attempt ID to see the list of all containers running the Flink jobs.

   * Click the log link for any container to view that container's log file (.log), standard output (stdout), and standard error output (stderr). These files typically contain the runtime or error logs of the Flink job.

2. Flink Web interface:

   * Open the YARN ResourceManager Web interface.

   * Locate the Application ID corresponding to your Flink job in the interface.

   * Click this Application ID to enter the application's details page.

   * On the details page, click the hyperlink after "Tracking URL". Normally, this will automatically redirect to the Flink Web interface.

   * In the Flink Web interface, click the "Job Manager" menu on the left to access the Job Manager details page.

   * On the Job Manager details page, click the "Logs" or "Log List" tab to view logs related to the Job Manager.

   * In the Flink Web interface, click the "Task Managers" page on the left to see the list of all TaskManagers.

   * Click any TaskManager, then click "Stdout", "Logs", or "Log List" to view the corresponding logs.

3. Using the YARN command\-line tool:

   * Open the YARN ResourceManager Web interface.

   * Locate the Application ID corresponding to your Flink job in the interface.

   * In the EMR console, select an ECS node from the MasterGroup and connect to it remotely.

   * Use the YARN command\-line tool `yarn logs` and run the command `yarn logs -applicationId <Application-ID>` to obtain logs (including all logs from the Job Manager and Task Manager).


Refer to the three methods above to view logs for Flink jobs that are currently running. In general, it is recommended to use the YARN ResourceManager Web interface and the Flink Web interface for viewing logs.

<span id="1e752a15"></span>
## Q7: How to view logs for completed Flink jobs?

For Flink jobs running on Hadoop YARN, once the job is finished, its logs are usually aggregated by YARN and stored in HDFS. This is achieved through YARN's log aggregation feature (the YARN service provided by Volcano Engine EMR enables this feature by default). The following are the main steps for viewing logs of completed Flink jobs:


1. YARN ResourceManager Web interface:

   * Open the YARN ResourceManager Web interface.

   * Locate the Application ID corresponding to your Flink job in the interface.

   * Click this Application ID to enter the application's details page.

   * On the details page, find the "Attempt ID" with the start time closest to the current time.

   * Click this Attempt ID to see the list of all containers that have ever run this Flink job.

   * Click any container's log link to view the container's log file (.log), standard output (stdout), and standard error output (stderr). These files typically contain the runtime or error logs of the Flink job.

2. Use the YARN command\-line tool:

   * Open the YARN ResourceManager web interface.

   * Locate the Application ID corresponding to your Flink job in the interface.

   * In the EMR console, select an ECS node from the MasterGroup and connect to it remotely.

   * Use the YARN command\-line tool `yarn logs` and run the command `yarn logs -applicationId <Application-ID>` to retrieve logs (including all logs from the Job Manager and Task Manager).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The retention period for completed logs is controlled by <code>yarn.log-aggregation.retain-seconds</code>. If this time is exceeded, the logs may have been automatically deleted. To retain logs for a longer period, adjust this parameter.</div>


<div data-tips="true" data-tips-type="tip">If the log files are very large, using the <code>yarn logs</code> command may take a long time to download and display the logs.</div>
