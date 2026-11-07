---
title: "ClickHouse C# Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/clickhouse-c-driver"
---

[ClickHouse.Client](https://github.com/DarkWanderer/ClickHouse.Client) is a .NET client for ClickHouse that enables developers to connect their applications to ByteHouse. It provides a straightforward way to perform data querying and manipulation within the .NET ecosystem, making it ideal for building data\-driven applications. This guide will walk you through the installation process, show you how to establish a connection, and provide code examples for basic operations. For further introduction, please refer to its [official documentation](https://github.com/DarkWanderer/ClickHouse.Client/wiki/Quick-start).

<span id="70bd6b5e"></span>
# Environment requirements

We recommend using .NET 6.0 or later.

<span id="1366381b"></span>
# Recommended version


|**Items** |**Verified versions/important notes** |
|---|---|
|DarkWanderer/ClickHouse.Client |7.10+ |
|DapperLib/Dapper |2.1.66 |
|dotnetcore/FreeSql |3.5.213 |


<span id="a41e95d9"></span>
# Restrictions


* ByteHouse JSONB and BitMap types are not supported.

* FreeSQL does not support UseAutoSyncStructure being set to True.

* Dapper does not support overriding the virtual warehouse setting that is already defined in the connection string.

* If you encounter other restrictions, contact the ByteHouse team for assistance.


<span id="f1055582"></span>
# Install drivers

```Bash
# Driver
dotnet add package ClickHouse.Client

# Dapper ORM
dotnet add package Dapper

# FreeSQL ORM
dotnet add package FreeSql.Provider.ClickHouse
```


<span id="8412294e"></span>
# Obtain ByteHouse connection information

ByteHouse supports connecting to the ClickHouse C# Driver through IAM users or database users. The following content describes the differences between IAM and database users to help you choose the right option for your use case


* **IAM user** is a user created in BytePlus Access Control (IAM), whose privileges are determined by IAM policies and the privileges you grant for ByteHouse resources and data. IAM users can access the ByteHouse Console. Access to ByteHouse is also supported through the CLI, connection drivers, ecosystem tools, and APIs.

* **Database user** is a database\-level user created in ByteHouse who can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse console, but they can access ByteHouse through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="3b54c987"></span>
## Use an IAM user to connect to ByteHouse

```Bash
"Protocol=https;Host={HOST};Port=8123;Database={DATABASE};Username=bytehouse;Password={API_KEY};"
```



|Param |Connect using IAM user |
|---|---|
|Host |When connecting to ByteHouse, the URL must use HTTPS and should be set to ByteHouse's public or private domain name. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |Set this to the fixed value 8123. |
|Username & Password |* username: Fixed as bytehouse<br><br>* password: ByteHouse API Key. You can obtain the API Key in the ByteHouse Console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|Database |The name of the database you want to connect to. |


<span id="4521e476"></span>
## Use a database user to connect to ByteHouse

```Bash
"Protocol=https;Host={HOST};Port=8123;Database={DATABASE};Username={accountID_or_accountName}::{username}::{envID};Password={password};"
```



|Param |Connect using a database user |
|---|---|
|Host |When connecting to ByteHouse, the URL must use HTTPS and be set to ByteHouse's public or private domain name. You can view and copy the network information in the ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|Port |Configured as the fixed value 8123. |
|Username & Password |* username is configured as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90).<br><br>   * `{accountID_or_accountName}`: Refers to the BytePlus user account ID or name. Log in to the ByteHouse Console, click Personal Center in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: Refers to the username used to log in to the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional configuration, the name of the environment where the database is located. No configuration is required when using the default environment. To use other environments, specify the environment name without adding `[]` during configuration. You can log in to the **ByteHouse** **Console** and find it under **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Configuration environment ID: `21xxxxxxxx::demouser::demoenv`<br><br>      * Environment ID not configured: `21xxxxxxxx::demouser`<br><br>* password: Contact the administrator to obtain the password for the database account. To reset your password if you have lost or forgotten it, contact the administrator. For details, please refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|Database |The name of the database you want to connect to. |


<span id="572c43fa"></span>
# Basic usage

You can use the following code to connect to ByteHouse and start developing on ByteHouse using standard statements for querying, writing, and reading data.


* Timeout configuration: Timeout defaults to 120s.


<span id="56453c7d"></span>
## Use the Dapper connection

<span id="940f97c7"></span>
### Connect ByteHouse

Use the following code to connect to ByteHouse. When using the code, make sure to replace the `{Host}`, `{Username}`, `{Password}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields in the connection statement. For instructions on how to obtain these fields, see [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/clickhouse-c-driver#8412294e).

```Go
    const string Host = "{Host}";
    const int Port = 8123;
    const string Password = "{Password}";
    const string Username = "{Username}";
    const string Database = "{Database}";
    const string Virtual_warehouse_id = "{Virtual_warehouse_id}";

    // Connection settings (update with your ClickHouse details)
    var connectionString = $"Protocol=https;Host={Host};Port=8123;Database={Database};Username={Username};Password={Password};set_virtual_warehouse={Virtual_warehouse_id}"; 
    return new ClickHouseConnection(connectionString);
```


<span id="fbe11460"></span>
### Use custom Query ID

```Go
    static void DropTable()
    {
        using (var connection = GetClickHouseConnection())
        {
            connection.Open();
            connection.CustomSettings.Add("query_id", $"customized_{Guid.NewGuid()}");
            connection.Execute(DropTableQuery);
        }
    }
```


<span id="6c4c88b3"></span>
### Connect to ByteHouse and query data

```Java
using System.Data;
using ClickHouse.Client.ADO;
using Dapper;

namespace ClickHouse.Client.DapperExample;

public static class DapperExample
{

    const string Host = "{Host}";
    const int Port = 8123;
    const string Password = "{Password}";
    const string Username = "{Username}";
    const string Database = "{Database}";
    const string Virtual_warehouse_id = "{Virtual_warehouse_id}";

    // Constants for SQL queries
    const string DropTableQuery = "DROP TABLE IF EXISTS users;";

    const string CreateTableQuery = @"
        CREATE TABLE users
        (
            Id UInt32,
            Name String,
            Email String
        ) ENGINE = CnchMergeTree()
        ORDER BY Id;
    ";

    const string InsertDataQuery = @"
        INSERT INTO users (Id, Name, Email) VALUES 
        (1, 'Alice', 'alice@example.com'), 
        (2, 'Bob', 'bob@example.com');
    ";

    const string SelectUsersQuery = "SELECT Id, Name, Email FROM users";

    public static void Main(string[] args)
    {
        try
        {
            // Drop table if exists
            DropTable();
            Console.WriteLine("Table dropped successfully.");

            // Create table
            CreateTable();
            Console.WriteLine("Table created successfully.");

            // Insert data
            InsertData();
            Console.WriteLine("Data inserted successfully.");

            // Retrieve and display data
            var users = GetUsers();
            foreach (var user in users)
            {
                Console.WriteLine($"Id: {user.Id}, Name: {user.Name}, Email: {user.Email}");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An error occurred: {ex.Message}");
        }
    }

    // Method to get the ClickHouse connection
    static ClickHouseConnection GetClickHouseConnection()
    {
        // Connection settings (update with your ClickHouse details)
        var connectionString = $"Protocol=https;Host={Host};Port=8123;Database={Database};Username={Username};Password={Password};set_virtual_warehouse={Virtual_warehouse_id}"; 
        return new ClickHouseConnection(connectionString);
    }

    // Method to drop the 'users' table if it exists
    static void DropTable()
    {
        using (var connection = GetClickHouseConnection())
        {
            connection.Open();
            connection.CustomSettings.Add("query_id", $"customized_{Guid.NewGuid()}");
            connection.Execute(DropTableQuery);
        }
    }

    // Method to create the 'users' table
    static void CreateTable()
    {
        using (var connection = GetClickHouseConnection())
        {
            connection.Open();
            connection.CustomSettings.Add("query_id", $"customized_{Guid.NewGuid()}");
            //Overwriting the global virtual_warehouse settings is not supported            //connection.CustomSettings.Add("virtual_warehouse", $"{Virtual_warehouse_id}");
            connection.Execute(CreateTableQuery);
        }
    }

    // Method to insert data into the 'users' table
    static void InsertData()
    {
        using (var connection = GetClickHouseConnection())
        {
            connection.Open();
            connection.Execute(InsertDataQuery);
        }
    }

    // Method to retrieve users from the 'users' table
    static IEnumerable<User> GetUsers()
    {
        using (var connection = GetClickHouseConnection())
        {
            connection.Open();
            return connection.Query<User>(SelectUsersQuery);
        }
    }

    // User class representing the 'users' table schema
    class User
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Email { get; set; }
    }
}
```


<span id="a0163716"></span>
## Use FreeSQL to connect

Refer to the following code to connect to ByteHouse. Caution: When using the code, replace the following fields in the connection statement: `{Host}`, `{Username}`, `{Password}`, `{Database}`, `{VIRTUAL_WAREHOUSE_ID}`, and other connection information fields. For instructions on how to obtain these fields, please refer to [Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/clickhouse-c-driver#8412294e).

<span id="6c3a5de7"></span>
### Connect ByteHouse

```Go
    const string Host = "{Host}";
    const int Port = 8123;
    const string Password = "{Password}";
    const string Username = "{Username}";
    const string Database = "{Database}";
    const string Virtual_warehouse_id = "{Virtual_warehouse_id}";

    // Configure FreeSql
    fsql = new FreeSqlBuilder()
        .UseConnectionString(DataType.ClickHouse, $"Protocol=https;Host={Host};Port={Port};Username={Username};Password={Password};Database={Database};set_virtual_warehouse={Virtual_warehouse_id}") 
        .UseAutoSyncStructure(false) // ByteHouse does not support setting this to true yet
        .Build();
```


<span id="f84bbfbd"></span>
### Connect to ByteHouse and query data

```C++
using FreeSql;
using FreeSql.DataAnnotations;

namespace ClickHouse.Client.FreeSQLExample;

public static class FreeSQLExample
{
    private static IFreeSql fsql;

    const string Host = "{Host}";
    const int Port = 8123;
    const string Password = "{Password}";
    const string Username = "{Username}";
    const string Database = "{Database}";
    const string Virtual_warehouse_id = "{Virtual_warehouse_id}";
    public static void Main(string[] args)
    {
        // Configure FreeSql
        fsql = new FreeSqlBuilder()
            .UseConnectionString(DataType.ClickHouse, $"Protocol=https;Host={Host};Port={Port};Username={Username};Password={Password};Database={Database};set_virtual_warehouse={Virtual_warehouse_id}") //To log in with a database account, update the connection string as described in the connection information section.
            .UseAutoSyncStructure(false) // ByteHouse does not support setting this to true yet
            .Build();
        
        // Execute DDL statement to create the table if it doesn't exist
        CreateTable();
        
        // Perform operations
        InsertUser();
        BulkInsertUsers();
        QueryUsers();
    }
     
    // Method to execute DDL statement
    static void CreateTable()
    {
        var createTableSql = @"
            CREATE TABLE IF NOT EXISTS users (
                Id Int32,
                Name String,
                Email String
            ) ENGINE = MergeTree()
            ORDER BY Id";
        
        fsql.Ado.ExecuteNonQuery(createTableSql);
        Console.WriteLine("Table created or already exists.");
    }

    // Define the User entity with explicit table mapping
    [Table(Name = "users")]
    class User
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Email { get; set; }
    }

    // Insert a new user
    static void InsertUser()
    {
        var newUser = new User { Id = 0, Name = "John Doe", Email = "john.doe@example.com" };
        fsql.Insert(newUser).ExecuteAffrows();
        Console.WriteLine("User inserted.");
    }

    // Bulk insert users
    static void BulkInsertUsers()
    {
        var users = new List<User>();
        for (int i = 1; i <= 1000; i++)
        {
            users.Add(new User { Id = i, Name = $"John Doe {i}", Email = $"john.doe{i}@example.com" });
        }

        fsql.Insert(users).ExecuteAffrows();
        Console.WriteLine("Bulk insert completed.");
    }

    // Query users
    static void QueryUsers()
    {
        var users = fsql.Select<User>().ToList();
        foreach (var user in users)
        {
            Console.WriteLine($"Id: {user.Id}, Name: {user.Name}, Email: {user.Email}");
        }
    }
}
```
