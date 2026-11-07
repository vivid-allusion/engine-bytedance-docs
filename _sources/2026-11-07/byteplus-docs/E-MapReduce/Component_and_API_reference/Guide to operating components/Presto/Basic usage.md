---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/presto_basic_usage"
---

Presto supports multiple operation modes. You can connect to Presto for SQL query analysis through Presto CLI, JDBC, Hue, Airflow, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR Presto enables LDAP authentication by default, so you need to provide the necessary authentication information when operating Presto. To disable LDAP authentication (not recommended), go to the console "<strong>Cluster details \> Service list \> Presto \> Service parameters</strong>" page, set the <code>presto.ldap-enabled</code> configuration item to false, and restart the Presto service.</div>


<span id="_1-使用前提"></span>
## **1. Prerequisites**


1. An E\-MapReduce (EMR) cluster has been created, including the Presto, Hue, and Airflow component services. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. If the Presto web UI access link is not clickable, check whether the ECS instance where Presto is located is bound to an elastic public IP. For details, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

3. To continue accessing, you need to add the source address and corresponding port to the allowlist in **Cluster Details \> Access Links \> Configure Service Ports**.


<span id="_2-presto-cli-使用"></span>
## 2 **Using Presto CLI**

To operate Presto through Presto CLI, first log in to the target cluster, then run the following command to enter the Presto interactive terminal:

For details on cluster login operations, see: [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

```bash
$ presto --user <username> --password
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The username and password parameters passed via the command line are imported or manually added in the user management page of the console. If LDAP authentication is not enabled, these parameters can be omitted.</div>



By default, EMR Presto reads the default\-cli.properties configuration file from the configuration directory and uses its contents to fill in missing command\-line parameters. You can also manually set parameters in the command line. Parameters specified in the command line take precedence over those in the default\-cli.properties configuration file.

After logging in to the Presto CLI interactive terminal, you can enter the required SQL statements in the terminal to execute query tasks. For example:

```plain
presto> select * from tpch.sf1.nation;
 nationkey |      name      | regionkey |                                                      comment
-----------+----------------+-----------+--------------------------------------------------------------------------------------------------------------------
         0 | ALGERIA        |         0 |  haggle. carefully final deposits detect slyly agai
         1 | ARGENTINA      |         1 | al foxes promise slyly according to the regular accounts. bold requests alon
         2 | BRAZIL         |         1 | y alongside of the pending deposits. carefully special packages are about the ironic forges. slyly special
         3 | CANADA         |         1 | eas hang ironic, silent packages. slyly regular packages are furiously over the tithes. fluffily bold
         4 | EGYPT          |         4 | y above the carefully unusual theodolites. final dugouts are quickly across the furiously regular d
         5 | ETHIOPIA       |         0 | ven packages wake quickly. regu
         6 | FRANCE         |         3 | refully final requests. regular, ironi
         7 | GERMANY        |         3 | l platelets. regular accounts x-ray: unusual, regular acco
         8 | INDIA          |         2 | ss excuses cajole slyly across the packages. deposits print aroun
         9 | INDONESIA      |         2 |  slyly express asymptotes. regular deposits haggle slyly. carefully ironic hockey players sleep blithely. carefull
        10 | IRAN           |         4 | efully alongside of the slyly final dependencies.
        11 | IRAQ           |         4 | nic deposits boost atop the quickly final requests? quickly regula
        12 | JAPAN          |         2 | ously. final, express gifts cajole a
        13 | JORDAN         |         4 | ic deposits are blithely about the carefully regular pa
        14 | KENYA          |         0 |  pending excuses haggle furiously deposits. pending, express pinto beans wake fluffily past t
        15 | MOROCCO        |         0 | rns. blithely bold courts among the closely regular packages use furiously bold platelets?
        16 | MOZAMBIQUE     |         0 | s. ironic, unusual asymptotes wake blithely r
        17 | PERU           |         1 | platelets. blithely pending dependencies use fluffily across the even pinto beans. carefully silent accoun
        18 | CHINA          |         2 | c dependencies. furiously express notornis sleep slyly regular accounts. ideas sleep. depos
        19 | ROMANIA        |         3 | ular asymptotes are about the furious multipliers. express dependencies nag above the ironically ironic account
        20 | SAUDI ARABIA   |         4 | ts. silent requests haggle. closely express packages sleep across the blithely
        21 | VIETNAM        |         2 | hely enticingly express accounts. even, final
        22 | RUSSIA         |         3 |  requests against the platelets use never according to the quickly regular pint
        23 | UNITED KINGDOM |         3 | eans boost carefully special requests. accounts are. carefull
        24 | UNITED STATES  |         1 | y final packages. slow foxes cajole quickly. quickly silent platelets breach ironic accounts. unusual pinto be
(25 rows)

Query 091124_00003_5sscg, FINISHED, 2 nodes
Splits: 32 total, 32 done (100.00%)
[Latency: client-side: 0:02, server-side: 0:02] [25 rows, 0B] [11 rows/s, 0B/s]
```


<span id="_3-jdbc-访问-presto"></span>
## 3 **Accessing Presto via JDBC**

To operate Presto using JDBC, you need to introduce the presto\-jdbc dependency. You can download the public version via Maven (as shown below), or obtain the presto\-jdbc dependency package compiled by EMR (located in the cluster directory `/usr/lib/emr/current/presto`).

```xml
<dependency>
    <groupId>com.facebook.presto</groupId>
    <artifactId>presto-jdbc</artifactId>
    <version>${latest_version}</version>
</dependency>
```


<span id="_3-1-使用编程方式"></span>
### 3.1 Using a programming approach

Using Java as an example, to access Presto via JDBC in your program code, refer to the following sample program, distinguishing whether LDAP authentication is enabled.


* **LDAP authentication enabled**

   ```java
   Properties props = new Properties();
   // The username and password are imported or created in user management
   props.setProperty("user", "<username>");
   props.setProperty("password", "<password>");
   props.setProperty("SSL", "true");
   // The keystore path corresponds to the http-server.https.keystore.path configuration item
   props.setProperty("SSLKeyStorePath", "<keystore_path>");
   // The keystore password corresponds to the http-server.https.keystore.key configuration item
   props.setProperty("SSLKeyStorePassword", "<keystore_password>");
   
   /** The connection address template is jdbc:presto://<host>:<port>, where:* - port is 8085 when LDAP authentication is enabled, and 8084 when LDAP authentication is not enabled;* - host is the hostname of the Coordinator, for example, emr-xxxxxx-master-1 */
   String url = "jdbc:presto://<coordinator_host>:8085";
   try (Connection connection = DriverManager.getConnection(url, props);
        Statement statement = connection.createStatement()) {
       ResultSet resultSet = statement.executeQuery("select * from tpch.sf1.nation");
       // ...
   }
   ```
   

* **LDAP authentication disabled**

   ```java
   Properties props = new Properties();
   // The username is imported or created in user management
   props.setProperty("user", "<username>");
   
   /** The connection address template is jdbc:presto://<host>:<port>, where:* - port is 8085 when LDAP authentication is enabled, and 8084 when LDAP authentication is not enabled;* - host is the hostname of the Coordinator, for example, emr-xxxxxx-master-1 */
   String url = "jdbc:presto://<coordinator_host>:8084";
   try (Connection connection = DriverManager.getConnection(url, props);
        Statement statement = connection.createStatement()) {
       ResultSet resultSet = statement.executeQuery("select * from tpch.sf1.nation");
       // ...
   }
   ```
   


After compiling the above program into a jar package, you can run it on your EMR cluster. If running outside the EMR cluster, note the following:


* You need to download the keystore file from the cluster to the location where your program runs, and modify the `keystore_path` parameter to point to your local keystore file.

* You must ensure connectivity between the node where your program runs and the EMR cluster's Presto Coordinator node, including both host and port connectivity.


<span id="_3-2-使用数据库管理工具"></span>
### 3.2 Using a database management tool

You can also connect to and access Presto locally using database management tools via JDBC. This section uses DBeaver as an example to explain how to configure a Presto database connection. To access the EMR cluster Presto service locally, you typically need to bind a public IP to the node where the Presto Coordinator is located, and determine whether LDAP authentication is enabled.


* **Enable LDAP authentication**

   1. Obtain the DNS information of the node where the Presto Coordinator is located by viewing "**Cluster details \- Node management**" in the console, for example:

   ```plain
   master-1-1.emr-d2bc787xxx.cn-beijing.emr-volces.com
   ```
   

   2. Verify local connectivity to the Presto service port **8085**. If the node where the Presto Coordinator is located does not have the port open to the local outbound IP, you can configure it in the ECS security group.

   3. Copy the keystore file of Presto from the cluster to your local machine. The location of the keystore file on the cluster can be obtained from the `http-server.https.keystore.path` configuration item in the Presto service parameters in the console.

   4. Configure the Presto database connection in DBeaver.

      In addition to entering the basic host, port, username, and password information, you also need to edit the driver properties and add the following configuration items:



|Parameter |Note |
|---|---|
|SSL |Enable SSL connection. The value is always set to true. |
|SSLKeyStorePath |The path to the locally downloaded keystore file |
|SSLKeyStorePassword |The corresponding keystore certificate key can be obtained through the `http-server.https.keystore.key` configuration item in the Presto service parameters on the console. |



* **Disable LDAP authentication**

1. Obtain the DNS information of the node where the Presto Coordinator is located by viewing "**Cluster details \- Node management**" in the console, for example `master-1-1.emr-d2bc7871c917fb2410de.cn-beijing.emr-volces.com`;

2. Verify local connectivity to the Presto service port **8084**. If the node where the Presto Coordinator is located does not have the port open to the local outbound IP, you can configure it in the ECS security group;

3. Configure the Presto database connection in DBeaver.


Connecting to the Presto service with LDAP authentication disabled is much simpler. You only need to configure the host, port, and username.

<span id="_4-hue-访问-presto"></span>
## 4 **Hue access to Presto**

You can submit Presto SQL statements for query analysis through the Hue interface. The user executing the SQL is the user who logs in to Hue. EMR Hue is automatically configured based on Presto configuration items by default, providing out\-of\-the\-box functionality. However, in the following situations, you need to manually restart the Hue service in the console to detect changes in Presto configuration items:


* Presto configuration items are changed, such as modifying Presto configuration parameters in the console.

* Presto is installed after Hue, since Presto is an optional service and manual installation cannot guarantee the installation order between the two.


After logging in and entering the Hue interactive page, you can run Presto SQL queries according to the following procedure:


1. Select Presto in the Hue Editor interface.

2. Enter Presto SQL statements in the SQL editor and submit for execution.

3. View the results.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8ee6bc9f105f9ddcc6359de9d91353a.png) </span>

<span id="_5-airflow-访问-presto"></span>
## 5 **Airflow access Presto**

To operate Presto through Airflow, you need to prepare the DAG file and upload it to the DAGs directory of Airflow. For details, refer to [Overview](https://docs.byteplus.com/docs/E-MapReduce/109188). Important:


* EMR Airflow has integrated Presto automatically and added a connection configuration with the ID presto. In the Presto DAG script you write, you must specify `conn_id=presto`.

* If you change the service configuration of Presto, you need to restart the Airflow WebServer to detect the updated Presto configuration items.


Presto DAG script example:

```python
from datetime import timedelta
import airflow
from airflow.hooks.presto_hook import PrestoHook
from airflow.operators.python_operator import PythonOperator

default_args = {
    'owner': 'airflow',
    'presto_conn_id': 'presto',
    'depends_on_past': False,
    'start_date': airflow.utils.dates.days_ago(0),
    'email': ['airflow@example.com'],
    'email_on_failure': True,
    'email_on_retry': False,
    'retries': 3,
    'retry_delay': timedelta(minutes=15),
}

dag = airflow.DAG('presto-demo',
                  default_args=default_args,
                  description='Presto Demo',
                  schedule_interval=timedelta(minutes=30)
                  )

ph = PrestoHook(presto_conn_id='presto',
                catalog='hive',
                schema='default',
                port=8080
                )


def presto_create_table(**context):
    sql = """CREATE TABLE IF NOT EXISTS tb_airflow_demo(id int, name varchar)"""
    data = ph.get_records(sql)
    return True


def presto_insert_data(**context):
    sql = """INSERT INTO tb_airflow_demo SELECT 1, 'name1' """
    data = ph.get_records(sql)
    return True


def presto_select_data(**context):
    sql = """SELECT * FROM tb_airflow_demo LIMIT 20"""
    data = ph.get_records(sql)
    return True


presto_create_table_task = PythonOperator(
    task_id='presto-create_table',
    provide_context=True,
    python_callable=presto_create_table,
    dag=dag
)

presto_insert_data_task = PythonOperator(
    task_id='presto_insert_data',
    provide_context=True,
    python_callable=presto_insert_data,
    dag=dag
)

presto_select_data_task = PythonOperator(
    task_id='presto_select_data',
    provide_context=True,
    python_callable=presto_select_data,
    dag=dag
)

presto_create_table_task >> presto_insert_data_task >> presto_select_data_task

if __name__ == "__main__":
    dag.cli()
```


After uploading the above script to the DAGs directory of Airflow, you can see the corresponding DAG task on the Airflow management page, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2a620fdb3a8a9c60dce796f30ee2d83.png) </span>
