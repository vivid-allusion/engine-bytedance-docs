---
title: "ByteHouse CLI"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-gateway-client"
---

ByteHouse CLI is a command\-line application used to interact with Bytehouse services in the most direct way. You can connect to ByteHouse CLI using keys and perform operations such as resource creation management and SQL queries. This tutorial will guide you through the steps of installing and using ByteHouse CLI.

<span id="0cf07f43"></span>
## Preparation

If you are using macOS, install Homebrew first. This tutorial uses Homebrew to install ByteHouse CLI. Refer to the official website for how to install Homebrew.

<span id="3bf1a375"></span>
## Installation

You can obtain the latest ByteHouse CLI release version from [the official GitHub repository](https://github.com/bytehouse-cloud/cli/releases/).

<span id="de3d3df6"></span>
### Install ByteHouse CLI using Homebrew on macOS

<span id="e58a01a3"></span>
#### Installation

Open your terminal and run the following command to install ByteHouse CLI.

```shell
brew tap bytehouse-cloud/homebrew-core
brew install bytehouse-cli
```


After installation, you can check the current installed version using the command below to ensure the installation is complete.

```Shell
bytehouse-cli -v
```


Query result example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff182cf7eecd463792a87c702d2ad4e7~tplv-goo7wpa0wc-image.image) </span>

<span id="874a892f"></span>
#### Upgrade

If you want to upgrade your ByteHouse CLI version, you can run the following command.

```shell
brew upgrade bytehouse-cli
```


<span id="44144527"></span>
#### Troubleshooting

If you have already installed ByteHouse CLI and encounter some errors during reinstallation or upgrade, try the following steps for troubleshooting.


1. Uninstall ByteHouse CLI.

   ```Go
   brew uninstall bytehouse-cli
   brew untap bytehouse-cloud/homebrew-core
   ```
   

2. Run the following command to reinstall.

   ```Go
   brew tap bytehouse-cloud/homebrew-core
   brew install bytehouse-cli
   ```
   


<span id="464dc4a2"></span>
### Linux System

For Linux systems, obtain the link to the latest release from the GitHub release page, replace the placeholder link in the following script and run it to install.

```shell
*# Obtain the latest link from the release address above, or replace the version number in the code below.
# Replace the first line below with the latest release version
curl -o bytehouse-cli.tar.gz -L https://github.com/bytehouse-cloud/cli/releases/download/<version>/bytehouse-cli_<version>_Linux_x86_64.tar.gz
mkdir -p ./bytehouse-cli/   # Replace this link address or version number
tar -zxvf bytehouse-cli.tar.gz -C ./bytehouse-cli
chmod +x bytehouse-cli 

# Add this binary executable to your `~/.bashrc` as alias, or `~/.zshrc`l
echo "alias bytehouse-cli=\"$(pwd)/bytehouse-cli\"" >> ~/.bashrc
```


<span id="7d3e57e2"></span>
### Windows System

For Windows systems, select the latest version from [the GitHub page](https://github.com/bytehouse-cloud/cli/releases), download the installation package, and then extract and install it.

The example format of the downloaded compressed package is as follows: `bytehouse-cli_1.26.8_Windows_x86_64.zip`.

<span id="430f8deb"></span>
## Connect to ByteHouse

ByteHouse supports connection using IAM users or database users. The differences between IAM users and database users are described below. Choose the user type that best fits your needs.


* **IAM User** is a user created in BytePlus Identity and Access Management (IAM). The user's privileges are determined by IAM privilege policies and the ByteHouse resource and data privileges you grant. IAM users can access the ByteHouse Console, and ByteHouse also supports access through CLI, connection drivers, ecosystem tools, API, and other methods.

* **Database User** is a database\-level user created in ByteHouse and can be granted environment, resources, and data privileges. Database users cannot access the ByteHouse Console, but access to ByteHouse is supported through CLI, connection drivers, ecosystem tools, API, and many other methods.


For more information about IAM users and database users, refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="cc2bee76"></span>
### Use an IAM user to connect

Use the following command to connect:

```Bash
bytehouse-cli --host {HOST} --port 19000 --secure --token {API_KEY} 
```


The example is as follows:

```bash
bytehouse-cli --host tenant-{TENANT_ID}-{REGION}-{ENVIRONMENT}-public.bytehouse.bytepluses.com --port 19000 --secure --token XXXXXXXXXXXXX

# more configuration parameter examples
bytehouse-cli --host tenant-{TENANT_ID}-{REGION}-{ENVIRONMENT}-public.bytehouse.bytepluses.com --port 19000 --secure --token XXXXXXXXXXXXX --send_timeout=3600 --read_timeout=3600 --virtual_warehouse=warehouse1 --database=db1
```


The parameters are explained below; for more flags and abbreviations, please refer to [CLI Configuration](https://docs.byteplus.com/docs/bytehouse/docs-cli-configuration).


|Parameter |Required |Configuration Description |
|---|---|---|
|`--host` |Yes |The cluster access address and port. You can view the network group configuration in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|`--port` |Yes |Port number for cluster access address. The default port is 19000. For ports used by other common connection methods, see [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers#18dc0302). |
|`--token` |Yes |Cluster access key, configured as API Key. You can log in to the ByteHouse console, go to the **Tenant management** \> **Connection information** page, and click the **API Key** section’s **New** button to create an API Key.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">API Key <strong>cannot be viewed again after creation</strong>. It is recommended to download the key for local storage.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can create up to 2 API Keys.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Keys need to be refreshed within 90 days to ensure security.</div><br> |
|`--secure` |No |Specify whether to use Secure TCP connection. If connecting to ByteHouse hosted on BytePlus, `--secure` is required. Default is true. |
|`--read_timeout` |No |Sets the read timeout from the server. Default: 300 seconds, which is 5 minutes. |
|`--send_timeout` |No |Sets the write timeout from the server. Default: 300 seconds, which is 5 minutes. |
|`--virtual_warehouse` |No |Specifies the virtual warehouse to use. The default is the user's default virtual warehouse, if available. |
|`--database` |No |Specifies the database to use. The default is the user's default database, if available. |


<span id="b775d23c"></span>
### Use a database user to connect

You can refer to the following command to connect:

```Bash
bytehouse-cli --user {accountID_or_accountName}::{username}::{envID} --password {password} --host {HOST} --port 19000 --secure 
```


The example is as follows:

```Bash
bytehouse-cli --user 21XXXXXXXX::demodb::testenv --password XXXXXXXX--host tenant-{TENANT_ID}-{REGION}-{ENVIRONMENT}-public.bytehouse.bytepluses.com --port 19000 --secure
```


Parameter descriptions are as follows. For more flags and their abbreviations, refer to [CLI Configuration](https://docs.byteplus.com/docs/bytehouse/docs-cli-configuration).


|Parameter |Required |Configuration Description |
|---|---|---|
|`--user` |Yes |The account of the database user. Set the user as `{accountID_or_accountName}::{username}[::{envID}]`. For details, see [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889):<br><br><br>* `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click the personal center at the top right to view and copy the account ID or name.<br><br>* `{username}`: It refers to the username for logging into the ByteHouse database. You can find it in the **ByteHouse Console** \> **Access control** \> **Users** \> **View Database user name**.<br><br>* `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>   Examples:<br><br>   * Default env: `30xxxxxxxx::demouser`<br><br>   * Other env: `30xxxxxxxx::demouser::demoenv` |
|`--password` |Yes |The password of the current database user. Contact the administrator to obtain the database account password. If the password is lost or forgotten, contact the administrator to reset it. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|`--host` |Yes |The cluster access address and port. You can view the network group configuration in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|`--port` |Yes |Port number for cluster access address. The default port is 19000. For ports used by other common connection methods, see [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers#18dc0302). |
|`--secure` |No |Specify whether to use Secure TCP connection. If connecting to ByteHouse hosted on BytePlus, `--secure` is required. This flag is enabled by default. |


<span id="e910a99b"></span>
## Non\-interactive mode

When writing shell scripts, you may need to run commands non\-interactively. bytehouse\-cli allows users to execute SQL commands and log out automatically.

<span id="dfacc2dd"></span>
### Use query flag

If you launch bytehouse\-cli with the \-q or \-\-query flag, it executes the given SQL statement and then exits immediately.

```bash
bytehouse-cli --host {HOST} --port 19000 --secure --token {API_KEY} -q "select 1" 
```


<span id="49e3bbf2"></span>
### Use stdin

You can also provide input to bytehouse\-cli via stdin.

```shell
echo "select 1" | bytehouse-cli
```


<span id="49ca808d"></span>
### Write scripts

You can also write SQL scripts and pipe the input through to the bytehouse CLI:


* Queries are separated with `;`.

* Queries will run in sequence.

* If a query returns an error, subsequent queries in the script will not be executed.


```shell
$ cat example.sql
CREATE DATABASE bob_db;
USE bob_db;
CREATE TABLE bob_number
(
   i Int32
)
ENGINE = CnchMergeTree
ORDER BY i;
SHOW CREATE TABLE bob_number;

$ bytehouse-cli < example.sql

# This is also accepted
$ cat example.sql | bytehouse-cli
```


<span id="2405de23"></span>
## Insert data

Loading data from files is a common task. Here are some examples:

<span id="ea458329"></span>
### **Insert data from a query**

<span id="0d2cb49f"></span>
#### Interactive mode

```SQL
Bytehouse » INSERT INTO bob_db.bob_number VALUES (1), (2), (3) 
```


<span id="015931d0"></span>
#### Non\-interactive mode

```SQL
$ bytehouse-cli -q "INSERT INTO bob_db.bob_number VALUES (1), (2), (3)"
```


<span id="4fad8479"></span>
### Insert data from a local file

<span id="61c16ecb"></span>
#### Interactive mode

```sql
Bytehouse » INSERT INTO bob_db.bob_number FORMAT csv INFILE 'path/to/data.csv'
```


<span id="6944dd7c"></span>
#### Non\-interactive mode

```shell
$ bytehouse-cli -q "INSERT INTO bob_db.bob_number FORMAT csv" < 'path/to/data.csv'
```


<span id="3a6a3fc1"></span>
## Data export

After a query executes, you can save the results to a local file using the INTO OUTFILE syntax. The file is saved to a path relative to the directory where you launched bytehouse\-cli.

```sql
Bytehouse » SELECT * FROM bob_db.bob_number INTO OUTFILE 'out.csv' format csv
```


If you need to keep the header of the query results, export in CSVWithNames format:

```sql
Bytehouse » SELECT * FROM bob_db.bob_number INTO OUTFILE 'out.csv' format CSVWithNames
```


<span id="230b0bd0"></span>
## Version check

You can check the version of ByteHouse CLI using the \-v or \-\-version flag. When this flag is specified, bytehouse\-cli prints the version and exits without launching an interactive session.

```shell
$ bytehouse-cli -v
v1.5.2
```


<span id="a1c56ee6"></span>
## Help

Use the `-h` flag or `--help` to display all supported flags

```bash
#To display all options and their alias
bytehouse-cli -h    
```
