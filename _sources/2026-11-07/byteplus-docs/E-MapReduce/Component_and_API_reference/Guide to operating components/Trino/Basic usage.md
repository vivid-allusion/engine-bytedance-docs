---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/trino_basic_usage"
---

Trino supports multiple operation modes. You can connect to Trino for SQL query analysis through Trino CLI, JDBC, HUE, and Airflow.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR Trino enables LDAP authentication by default, so you must provide the necessary authentication information when operating Trino. To disable LDAP authentication (not recommended), go to the console page <strong>Cluster details \> Service list \> Trino \> Service parameters</strong>, set the <code>trino.ldap-enabled</code> configuration item to false, and restart the Trino service.</div>


<span id="_1-使用前提"></span>
## **1 Prerequisites**


1. An E\-MapReduce (EMR) cluster has been created and includes the Trino, Hue, and Airflow component services. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. If the Trino web UI access link cannot be clicked, check whether the ECS instance where Trino is located is bound to an Elastic Public IP. For details, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

3. You need to add the source address and corresponding port to the allowlist in **Cluster details \> Access links \> Configure service ports** before you can continue to access.


<span id="_2-trino-cli-使用"></span>
## 2 Using Trino CLI

To access and operate Trino through Trino CLI, log in to the target cluster first, then execute the following command to enter the Trino interactive terminal:

For details on cluster login operations, see: [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

```bash
$ trino --user <username> --password
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The username and password parameters passed from the command line are imported or manually added by you in the user management page of the console. If LDAP authentication mode is not enabled, you may omit them.</div>



EMR Trino will, by default, read the default\-cli.properties configuration file from the configuration directory and use the contents of this file to fill in missing command\-line parameters. Of course, you can also actively set parameters in the command line. Parameters specified in the command line take precedence over those in the default\-cli.properties configuration file.

After logging in to the Trino CLI interactive terminal, you can enter the SQL statements to execute query tasks in the terminal, for example:

```bash
trino> select * from tpch.sf1.nation;
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

Query 085720_00001_abdsb, FINISHED, 2 nodes
Splits: 16 total, 16 done (100.00%)
1.65 [25 rows, 0B] [15 rows/s, 0B/s]
```


<span id="_3-jdbc-访问-trino"></span>
## 3 JDBC access to Trino

To operate Trino using JDBC, you need to first introduce the trino\-jdbc dependency. You can download the public version via Maven (as shown below), or obtain the trino\-jdbc dependency package compiled by EMR (located in the cluster `/usr/lib/emr/current/trino` directory).

```xml
<dependency>
    <groupId>io.trino</groupId>
    <artifactId>trino-jdbc</artifactId>
    <version>${latest_version}</version>
</dependency>
```


<span id="_3-1-使用编程方式"></span>
### 3.1 Using programming methods

Using Java as an example, to access Trino via JDBC in your program code, refer to the following sample program and distinguish whether LDAP authentication is enabled.


* **Enable LDAP authentication**


```java
Properties props = new Properties();

// The username and password are imported or created in user management.
props.setProperty("user", "<username>");
props.setProperty("password", "<password>");
props.setProperty("SSL", "true");
// The keystore path corresponds to the http-server.https.keystore.path configuration item.
props.setProperty("SSLKeyStorePath", "<keystore_path>");
// The keystore password corresponds to the http-server.https.keystore.key configuration item.
props.setProperty("SSLKeyStorePassword", "<keystore_password>");

/** The connection address template is jdbc:trino://<host>:<port>, where:* - port is 9085 when LDAP authentication is enabled, and 9084 when LDAP authentication is not enabled.* - host is the hostname of the Coordinator, for example, master-1-1.emr-e9193fb05ae1e3477d99.cn-beijing.emr-volces.com */
String url = "jdbc:trino://<coordinator_hostname>:9085";
try (Connection connection = DriverManager.getConnection(url, props);
     Statement statement = connection.createStatement()) {
    ResultSet resultSet = statement.executeQuery("select * from tpch.sf1.nation");
    // ...
}
```



* **Disable LDAP authentication**


```java
Properties props = new Properties();

// The username is imported or created in user management.
props.setProperty("user", "<username>");

/** The connection address template is jdbc:trino://<host>:<port>, where:* - port is 9085 when LDAP authentication is enabled, and 9084 when LDAP authentication is not enabled.* - host is the hostname of the Coordinator, for example, master-1-1.emr-e9193fb05ae1e3477d99.cn-beijing.emr-volces.com */
String url = "jdbc:trino://<coordinator_hostname>:9084";
try (Connection connection = DriverManager.getConnection(url, props);
     Statement statement = connection.createStatement()) {
    ResultSet resultSet = statement.executeQuery("select * from tpch.sf1.nation");
    // ...
}
```


After compiling the above program into a jar package, you can run it on your EMR cluster. If you are running outside the EMR cluster, note the following:


* You need to download the keystore file from the cluster to the location where your program runs, and modify the `keystore_path` parameter to point to your local keystore file.

* You need to ensure connectivity between the node where your program runs and the EMR cluster's Trino Coordinator node, including host connectivity and port connectivity.


<span id="_3-2-使用数据库管理工具"></span>
### 3.2 Using database management tools

JDBC also supports connecting to and accessing Trino locally using database management tools. This section uses DBeaver as an example to explain how to configure a Trino database connection. To access the Trino service of an EMR cluster locally, you typically need to bind a public IP address to the node where the Trino Coordinator is located, depending on whether LDAP authentication is enabled.


* **Enable LDAP authentication**

1. View and obtain the DNS information of the node where the Trino Coordinator is located through "**Cluster Details \- Node Management**" on the console, for example, `master-1-1.emr-``e9193fb05ae1e3477d99``.cn-beijing.emr-volces.com`;

2. Verify local connectivity to Trino service port **9085**. If the node where the Trino Coordinator is located does not have the port open to the local outbound IP, you can configure it in the ECS security group;

3. Copy the Trino keystore file from the cluster to your local machine. The location of the keystore file on the cluster can be obtained from the `http-server.https.keystore.path` configuration item in the Trino service parameters on the console;

4. Configure the Trino database connection in DBeaver as shown below:


In addition to entering the basic host, port, username, and password information, you also need to edit the driver properties and add the following configuration items:


|Parameter |Note |
|---|---|
|SSL |Enable SSL connection; the value must always be set to true. |
|SSLKeyStorePath |The path of the keystore file downloaded locally. |
|SSLKeyStorePassword |The corresponding keystore certificate key can be obtained from the `http-server.https.keystore.key` configuration item in the Trino service parameters on the console side. |



* **Disable LDAP authentication**

1. View and obtain the DNS information of the node where the Trino Coordinator is located through "**Cluster Details \- Node Management**" on the console, for example, `master-1-1.emr-``e9193fb05ae1e3477d99``.cn-beijing.emr-volces.com`;

2. Verify local connectivity to Trino service port **9084**. If the node where the Trino Coordinator is located does not have the port open to the local outbound IP, you can configure it in the ECS security group;

3. Configure the Trino database connection in DBeaver as shown below:


Connecting to the Trino service without LDAP authentication is much simpler; you only need to configure the host, port, and username.

<span id="_4-hue-访问-trino"></span>
## 4 **Access Trino via Hue**

You can submit Trino SQL statements for query analysis through the Hue interface. The user executing the SQL is the user logged in to Hue. By default, EMR Hue automatically configures itself based on Trino configuration items for out\-of\-the\-box use. However, in the following situations, you need to manually restart the Hue service in the console to detect changes in Trino configuration items:


* Trino configuration items have changed, such as when Trino configuration parameters are modified in the console.

* Trino is installed after Hue. Because Trino is an optional service, manual installation cannot guarantee the installation order of the two services.


After logging in and entering the Hue interactive page, you can run Trino SQL queries according to the following procedure:


1. Select Trino in the Hue Editor interface.

2. Enter Trino SQL statements in the SQL editor and submit them for execution.

3. View the execution results.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_afd82e89edca17a9013d6b292a36120a.png) </span>

<span id="_5-airflow-访问-trino"></span>
## 5 **Airflow access to Trino**

To operate Trino through Airflow, you need to edit the DAG file in advance and upload it to the DAGs directory of Airflow. For details, refer to [Overview](https://docs.byteplus.com/docs/E-MapReduce/109188). Caution:


* EMR Airflow has been automatically integrated with Trino, and a connection configuration with the ID trino has been added. In the Trino DAG script you write, you must specify `conn_id=trino`.

* If you change the service configuration of Trino, you need to restart the Airflow WebServer to detect the updated Trino configuration items.


Trino DAG script example:

```python
from datetime import timedelta
import airflow
from airflow.providers.trino.hooks.trino import TrinoHook
from airflow.operators.python_operator import PythonOperator

default_args = {'owner': 'airflow',
                'depends_on_past': False,
                'start_date': airflow.utils.dates.days_ago(0),
                'email': ['airflow@example.com'],
                'email_on_failure': True,
                'email_on_retry': False,
                'retries': 3,
                'retry_delay': timedelta(minutes=15)
                }

dag = airflow.DAG('trino-demo',
                  default_args=default_args,
                  description='Trino Demo',
                  schedule_interval=timedelta(minutes=30)
                  )

ph = TrinoHook(trino_conn_id='trino',
               catalog='hive',
               schema='default',
               port=8080
               )


def trino_drop_table(**context):
    sql = """DROP TABLE IF EXISTS tb_airflow_demo"""
    data = ph.get_records(sql)
    return True


def trino_create_table(**context):
    sql = """CREATE TABLE IF NOT EXISTS tb_airflow_demo(id int, name varchar)"""
    data = ph.get_records(sql)
    return True


def trino_insert_data(**context):
    sql = """INSERT INTO tb_airflow_demo SELECT 1, 'name1' """
    data = ph.get_records(sql)
    return True


def trino_select_data(**context):
    sql = """SELECT * FROM tb_airflow_demo LIMIT 20"""
    data = ph.get_records(sql)
    return True


# trino_drop_table_task = PythonOperator(task_id='trino_drop_table',provide_context=True,python_callable=trino_drop_table,dag=dag)
trino_create_table_task = PythonOperator(
    task_id='trino_create_table',
    provide_context=True,
    python_callable=trino_create_table,
    dag=dag
)

trino_insert_data_task = PythonOperator(
    task_id='trino_insert_data',
    provide_context=True,
    python_callable=trino_insert_data,
    dag=dag
)

trino_select_data_task = PythonOperator(
    task_id='trino_select_data',
    provide_context=True,
    python_callable=trino_select_data,
    dag=dag
)

trino_create_table_task >> trino_insert_data_task >> trino_select_data_task

if __name__ == "__main__":
    dag.cli()
```


After uploading the above script to the DAGs directory of Airflow, you can see the corresponding DAG task on the Airflow management page, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_171db140c076061f5fdfb4c769c66ae8.png) </span>
