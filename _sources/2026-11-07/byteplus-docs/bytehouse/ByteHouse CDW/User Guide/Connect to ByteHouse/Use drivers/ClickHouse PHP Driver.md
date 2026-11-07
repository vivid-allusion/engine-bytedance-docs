---
title: "ClickHouse PHP Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-bytehouse-php-connection"
---

The ClickHouse PHP driver allows your PHP applications to connect to the ByteHouse Cloud Data Warehouse. This document guides you through installing the driver, establishing a connection, and performing basic data operations like creating tables and executing queries.

<span id="21c2888c"></span>
# Environment requirements


|**Subitems** |**Verified Version** |
|---|---|
|ClickHouse driver version |Verified version: 1.6.0, for version details and download link, see: [phpClickhouse v1.6.0](https://github.com/smi2/phpClickHouse/releases/tag/1.6.0). |
|PHP version |Verified version: PHP 8.4 or higher |


<span id="c12ae82a"></span>
# Restrictions


* The JSONB and BitMap64 types of ByteHouse are not supported.

* KeepAlive setting is not supported.

* To resolve any other unknown restrictions encountered during use, please contact the ByteHouse team.


<span id="2d798f6c"></span>
# Install ClickHouse PHP driver

After obtaining the ClickHouse PHP driver, you can install it using `composer`:

```Bash
composer require smi2/phpclickhouse
```


<span id="cc4d2a7a"></span>
# Obtain ByteHouse connection details

ByteHouse supports connecting to the ClickHouse PHP driver through IAM users or database users. The differences between IAM users and database users are described as follows; you may choose according to your needs.


* **IAM user** is a user created in BytePlus Access Control (IAM), whose privileges are determined by IAM privilege policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. The IAM users can also access ByteHouse using CLI, connection drivers, ecosystem tools, APIs, and so on.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="b13ce652"></span>
## Use an IAM user to connect


|Parameter |Configuration description |
|---|---|
|host |Configure the public/private connection domain name for ByteHouse, where {TENANT_ID} and {REGION} refer to the BytePlus primary account ID and ByteHouse region information, respectively. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set this to the fixed value 8123. |
|database |Database name configured for connecting to ByteHouse. |
|user & password |* user: bytehouse (fixed configuration)<br><br>* password: The API Key for ByteHouse. You can obtain the API Key in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|https |Set this to true. |
|$db\-\>settings()\-\>set() |Optional. It is used to set ByteHouse server parameters, such as configuring the virtual warehouse used after connecting to ByteHouse. To use a specified virtual warehouse for subsequent ByteHouse data queries when you have multiple virtual warehouses, or to set other specified parameters, you can set them in `$db->settings()->set()`.<br><br>How to obtain a virtual warehouse ID: You can view the ID of the corresponding virtual warehouse on the **Virtual warehouse** page in the ByteHouse Console. |


<span id="d6446192"></span>
## Use database user connections


|Parameter |Configuration description |
|---|---|
|host |Configure the public or private network connection domain name for ByteHouse, where {TENANT_ID} and {REGION} correspond to the BytePlus user account ID and ByteHouse's region information, respectively. You can view and copy this information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|port |Set this to the fixed value 8123. |
|database |Database name configured for connecting to ByteHouse. |
|user & password |* The format for the user is `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: Refers to the BytePlus user account ID or name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: The username used to log in to the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. The name of the environment where the database is located. No configuration is required when using the default environment; to use another environment, you must specify the environment name, and do not include `[]` when configuring. You can log in to the **ByteHouse** **console** and obtain it from **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Example usage is as follows:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Do not configure environment ID: `21xxxxxxxx::demouser`<br><br>* password: Contact the administrator to obtain the password for the database account. To reset your password if you have lost or forgotten it, contact the administrator. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|https |The fixed configuration is: true. |
|$db\-\>settings()\-\>set() |Optional. It is used to set ByteHouse server\-related parameters, for example, to configure the virtual warehouse used after connecting to ByteHouse. To specify which virtual warehouse to use for subsequent ByteHouse queries when you have multiple virtual warehouses, or to set other parameters, you can set these in `$db->settings()->set()`.<br><br>How to obtain a virtual warehouse ID: You can view the ID of the corresponding virtual warehouse on the **Virtual warehouse** page in the ByteHouse Console. |


<span id="1e4dc44d"></span>
# Basic usage

After connecting to ByteHouse, you can create tables, read and write data, and perform other operations through the ClickHouse PHP Driver. The following is a simple example of these operations.

Timeout configuration: The default value of setConnectTimeOut is 5 seconds, the default value of setTimeout is 20 seconds, and the setTimeout configuration uses the max_execution_time parameter of ClickHouse.

<span id="f9def32e"></span>
## Connect ByteHouse

You can refer to the following code to connect to ByteHouse. Caution: When using the code, replace the fields in the connection statement—such as `{Host}`, `{User}`, `{Password}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields—with your actual connection details. For information on how to obtain these values, see [Obtain ByteHouse connection details](https://docs.byteplus.com/docs/bytehouse/docs-bytehouse-php-connection#cc4d2a7a).

```PHP
<?php

require_once 'vendor/autoload.php';

use Ramsey\Uuid\Uuid;

class Example
{
    private $client;
    private $config;

    public function __construct($host, $port, $user, $password, $database, $virtualWarehouse = null)
    {
        $this->config = [
            'host' => $host,
            'port' => $port,
            'username' => $user,
            'password' => $password,
            'database' => $database,
            'https' => true
        ];

        $this->initializeClient($virtualWarehouse);
    }

    private function initializeClient($virtualWarehouse)
    {
        try {
            $this->client = new ClickHouseDB\Client($this->config);
            if ($virtualWarehouse) {
                $this->client->settings()->set('virtual_warehouse', $virtualWarehouse);
            }
            $this->client->ping();
            $this->client->setTimeout(60);
            $this->client->setConnectTimeOut(10);

        } catch (Exception $e) {
            throw new Exception("初始化ClickHouse客户端失败: " . $e->getMessage());
        }
    }

    public function __destruct()
    {
        unset($this->client);
    }
}

try {
    $host = "{Host}";
    $port = 8123;
    $password = "{Password}";
    $user = "{User}";
    $database = "{Database}";
    $virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";

    $example = new Example($host, $port, $user, $password, $database, $virtual_warehouse_id);
    $example->runExample();

} catch (Exception $e) {
    echo "Program execution failed: " . $e->getTraceAsString() . "\n";
    exit(1);
}

?>
```


<span id="00ba203d"></span>
## Custom query ID

You can use the "set" command in settings to configure the session\-level query ID.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">With this method, you need to reset the query ID before each SQL execution.</div>


```Go
$this->client->settings()->set('query_id', 'customized_' . Uuid::uuid4()->toString());
```


<span id="3c4074ab"></span>
## Create a table and read/write data

```PHP
<?php

require_once 'vendor/autoload.php';

use Ramsey\Uuid\Uuid;

class Example
{
    private $client;
    private $config;

    public function __construct($host, $port, $user, $password, $database, $virtualWarehouse = null)
    {
        $this->config = [
            'host' => $host,
            'port' => $port,
            'username' => $user,
            'password' => $password,
            'database' => $database,
            'https' => true
        ];

        $this->initializeClient($virtualWarehouse);
    }

    private function initializeClient($virtualWarehouse)
    {
        try {
            $this->client = new ClickHouseDB\Client($this->config);
            if ($virtualWarehouse) {
                $this->client->settings()->set('virtual_warehouse', $virtualWarehouse);
            }
            $this->client->ping();
            $this->client->setTimeout(60);
            $this->client->setConnectTimeOut(10);

        } catch (Exception $e) {
            throw new Exception("初始化ClickHouse客户端失败: " . $e->getMessage());
        }
    }

    public function runExample()
    {
        try {
            $this->cleanupDatabase();
            $this->createTable();
            $this->insertData();
            $this->queryData();
            $this->cleanupTable();

        } catch (Exception $e) {
            throw $e;
        }
    }

    private function cleanupDatabase()
    {
        $queryId = 'customized_' . Uuid::uuid4()->toString();
        $this->client->write("DROP DATABASE IF EXISTS bhpythontest");
        $this->client->write("CREATE DATABASE IF NOT EXISTS bhpythontest");
        $this->client->database('bhpythontest');
        echo "Database cleaned up and creation completed\n";
    }

    private function createTable()
    {
        $sql = "
        CREATE TABLE IF NOT EXISTS bhpythontest.example (
            Col1 UInt8,
            Col2 String,
            Col3 FixedString(3),
            Col4 UUID,
            Col5 Map(String, UInt8),
            Col6 Array(String),
            Col7 Tuple(String, UInt8, Array(Map(String, String))) KV,
            Col8 DateTime
        ) ENGINE = CnchMergeTree() ORDER BY tuple()
        ";

        $this->client->write($sql);
        echo "Table created successfully\n";
    }

    private function insertData()
    {
        $start = microtime(true);
        $values = [];
        for ($i = 0; $i < 100; $i++) {
            $values[] = sprintf(
                "(42, 'ClickHouse', 'Inc', '%s', map('key', 1, 'key2', %d), ['Q','W','E','R','T','Y'], ('String Value', 5, [map('key','value')]), now())",
                Uuid::uuid4()->toString(),
                $i + 1
            );
        }

        $insertSQL = "INSERT INTO bhpythontest.example VALUES " . implode(', ', $values);
        $this->client->write($insertSQL);
        $time = microtime(true) - $start;
        echo sprintf("Records inserted successfully, time elapsed: %.2f seconds\n", $time);
    }

    private function queryData()
    {
        $result = $this->client->select("SELECT * FROM example LIMIT 5");

        if ($result->count() > 0) {
            echo "The first five records:\n";
            echo str_repeat("-", 80) . "\n";

            foreach ($result->rows() as $index => $row) {
                echo sprintf("Recors %d:\n", $index + 1);
                echo sprintf("  Col1: %d\n", $row['Col1']);
                echo sprintf("  Col2: %s\n", $row['Col2']);
                echo sprintf("  Col3: %s\n", $row['Col3']);
                echo sprintf("  Col4: %s\n", $row['Col4']);
                echo sprintf("  Col5: %s\n", json_encode($row['Col5']));
                echo sprintf("  Col6: %s\n", json_encode($row['Col6']));
                echo sprintf("  Col7: %s\n", json_encode($row['Col7']));
                echo sprintf("  Col8: %s\n", $row['Col8']);
                echo "\n";
            }
        }
    }

    private function cleanupTable()
    {
        $this->client->write("DROP TABLE IF EXISTS example");
        echo "Table cleaned up successfully.\n";
    }

    public function __destruct()
    {
        unset($this->client);
    }
}

try {
    $host = "{Host}";
    $port = 8123;
    $password = "{Password}";
    $user = "{User}";
    $database = "{Database}";
    $virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";

    $example = new Example($host, $port, $user, $password, $database, $virtual_warehouse_id);
    $example->runExample();

} catch (Exception $e) {
    echo "Program execution failed: " . $e->getTraceAsString() . "\n";
    exit(1);
}

?>
```


<span id="5aecec18"></span>
## Write data in batches via CSV files

You can use `insertBatchFiles()` to insert multiple CSV files in parallel, which enables efficient batch loading of data into ByteHouse.

```PHP
<?php

require_once 'vendor/autoload.php';

use Ramsey\Uuid\Uuid;

function generateDemoCSV($filename, $numRows): void
{
    $fp = fopen($filename, 'w');
    for ($i = 0; $i < $numRows; $i++) {
        fputcsv($fp, [
            date('Y-m-d'), // event_date
            rand(1000, 9999), // user_id
            'Message ' . $i, // message
            rand(1, 100) // value
        ], ',', '"', "\\", "\n");
    }
    fclose($fp);
    echo "Generated $numRows rows in $filename\n";
}

class Example
{
    private $client;
    private $config;

    public function __construct($host, $port, $user, $password, $database, $virtualWarehouse = null)
    {
        $this->config = [
            'host' => $host,
            'port' => $port,
            'username' => $user,
            'password' => $password,
            'database' => $database,
            'https' => true
        ];

        $this->initializeClient($virtualWarehouse);
    }

    private function initializeClient($virtualWarehouse)
    {
        try {
            $this->client = new ClickHouseDB\Client($this->config);

            if ($virtualWarehouse) {
                $this->client->settings()->set('virtual_warehouse', $virtualWarehouse);
            }

            $this->client->ping();
            $this->client->setTimeout(60);
            $this->client->setConnectTimeOut(10);

        } catch (Exception $e) {
            throw new Exception("Failed to initialize the ClickHouse client: " . $e->getMessage());
        }
    }

    public function runExample()
    {
        try {
            $this->cleanupDatabase();
            $this->insertIntoFromCSV();
        } catch (Exception $e) {
            throw $e;
        }
    }

    private function insertIntoFromCSV()
    {
        try {

            $this->client->write('DROP TABLE IF EXISTS demo_table');
            $this->client->write('
        CREATE TABLE demo_table (
            event_date Date,
            user_id UInt32,
            message String,
            value UInt32
        ) ENGINE = CnchMergeTree ORDER BY tuple()
    ');

            // Generate CSV files
            $files = [
                __DIR__ . '/demo_data_1.csv' => 1000,
                __DIR__ . '/demo_data_2.csv' => 1000
            ];

            foreach ($files as $file => $rows) {
                generateDemoCSV($file, $rows);
            }

            // Insert data via Batch Operation
            $result = $this->client->insertBatchFiles(
                'demo_table',
                array_keys($files),
                ['event_date', 'user_id', 'message', 'value']
            );

            $totalCount = $this->client->select('SELECT count() as count FROM demo_table')->fetchOne('count');
            echo "Total rows: $totalCount\n";

        } catch (\Exception $e) {
            echo "Error: " . $e->getMessage() . "\n";
        }
    }

    private function cleanupDatabase()
    {
        $this->client->write("DROP DATABASE IF EXISTS bhpythontest");
        $this->client->write("CREATE DATABASE IF NOT EXISTS bhpythontest");
        $this->client->database('bhpythontest');
        echo "Database cleaned up and creation completed\n";
    }

    public function __destruct()
    {

        unset($this->client);
    }
}


try {
    $host = "{Host}";
    $port = 8123;
    $password = "{Password}";
    $user = "{User}";
    $database = "{Database}";
    $virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";


    $example = new Example($host, $port, $user, $password, $database, $virtual_warehouse_id);
    $example->runExample();

} catch (Exception $e) {
    echo "Program execution failed: " . $e->getTraceAsString() . "\n";
    exit(1);
}

?>
```


<span id="74266d67"></span>
## Query data using parameter binding

Currently, both the `':param'` syntax and the `'{param}'` syntax are supported, allowing parameter values to be safely passed to queries using placeholders. Examples are as follows.

```PHP
<?php

require_once 'vendor/autoload.php';

use Ramsey\Uuid\Uuid;

function generateDemoCSV($filename, $numRows): void
{
    $fp = fopen($filename, 'w');
    for ($i = 0; $i < $numRows; $i++) {
        fputcsv($fp, [
            date('Y-m-d'), // event_date
            rand(1000, 9999), // user_id
            'Message ' . $i, // message
            rand(1, 100) // value
        ], ',', '"', "\\", "\n");
    }
    fclose($fp);
    echo "Generated $numRows rows in $filename\n";
}

class Example
{
    private $client;
    private $config;

    public function __construct($host, $port, $user, $password, $database, $virtualWarehouse = null)
    {
        $this->config = [
            'host' => $host,
            'port' => $port,
            'username' => $user,
            'password' => $password,
            'database' => $database,
            'https' => true
        ];

        $this->initializeClient($virtualWarehouse);
    }

    private function initializeClient($virtualWarehouse)
    {
        try {
            $this->client = new ClickHouseDB\Client($this->config);

            if ($virtualWarehouse) {
                $this->client->settings()->set('virtual_warehouse', $virtualWarehouse);
            }

            $this->client->ping();
            $this->client->setTimeout(60);
            $this->client->setConnectTimeOut(10);

        } catch (Exception $e) {
            throw new Exception("Failed to initialize the ClickHouse client: " . $e->getMessage());
        }
    }

    public function runExample()
    {
        try {
            $this->cleanupDatabase();
            $this->bindParamters();
        } catch (Exception $e) {
            throw $e;
        }
    }

    
    private function bindParamters()
    {
        try {
            // Create a sample table
            $this->client->write('DROP TABLE IF EXISTS user_events');
            $this->client->write('
        CREATE TABLE user_events (
            event_date Date,
            event_type String,
            user_id UInt32,
            score Float32,
            tags Array(String)
        ) ENGINE = CnchMergeTree ORDER BY tuple()
    ');
    
            // Insert sample data
            $this->client->insert('user_events', [
                [
                    '2024-01-01', 'login', 101, 0.5, ['new', 'mobile']
                ],
                [
                    '2024-01-01', 'purchase', 102, 0.8, ['vip', 'desktop']
                ],
                [
                    '2024-01-02', 'login', 101, 0.3, ['mobile']
                ]
            ], [
                'event_date', 'event_type', 'user_id', 'score', 'tags'
            ]);
    
            // Example 1: Basic parameter binding
            $result = $this->client->select(
                'SELECT * FROM user_events WHERE user_id = :id',
                ['id' => 101]
            );
            echo "Events for user 101:\n";
            print_r($result->rows());
    
            // Example 2: multiple parameter binding
            $result = $this->client->select(
                'SELECT * FROM user_events 
         WHERE event_date = :date AND event_type = :type',
                [
                    'date' => '2024-01-01',
                    'type' => 'login'
                ]
            );
            echo "\nLogin events on 2024-01-01:\n";
            print_r($result->rows());
    
            // Example 3: Bind Array
            $result = $this->client->select(
                'SELECT * FROM user_events 
         WHERE user_id IN (:users) AND score >= :min_score',
                [
                    'users' => [101, 102],
                    'min_score' => 0.5
                ]
            );
            echo "\nHigh-scoring events for selected users:\n";
            print_r($result->rows());
    
            // Example 4: Bind a template to a column query (template)
            $columns = 'event_date, event_type, user_id';
            $result = $this->client->select(
                'SELECT {cols} FROM user_events WHERE score > :score',
                [
                    'cols' => $columns,
                    'score' => 0.4
                ]
            );
            echo "\nSelected columns for high scores:\n";
            print_r($result->rows());
    
        } catch (\Exception $e) {
            echo "Error: " . $e->getMessage() . "\n";
        }
    
    }

    private function cleanupDatabase()
    {
        $this->client->write("DROP DATABASE IF EXISTS bhpythontest");
        $this->client->write("CREATE DATABASE IF NOT EXISTS bhpythontest");
        $this->client->database('bhpythontest');
        echo "Database cleaned up and creation completed\n";
    }

    public function __destruct()
    {

        unset($this->client);
    }
}


try {
    $host = "{Host}";
    $port = 8123;
    $password = "{Password}";
    $user = "{User}";
    $database = "{Database}";
    $virtual_warehouse_id = "{VIRTUAL_WAREHOUSE_ID}";


    $example = new Example($host, $port, $user, $password, $database, $virtual_warehouse_id);
    $example->runExample();

} catch (Exception $e) {
    echo "Program execution failed: " . $e->getTraceAsString() . "\n";
    exit(1);
}

?>
```
