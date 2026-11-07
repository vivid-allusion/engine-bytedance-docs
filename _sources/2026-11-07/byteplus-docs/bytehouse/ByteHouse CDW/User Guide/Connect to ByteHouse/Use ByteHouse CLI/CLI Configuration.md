---
title: "CLI Configuration"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-cli-configuration"
---

Currently, ByteHouse supports two methods for parameter configuration, namely configuration file and flag, This article will introduce these two methods in detail and provide a complete list of configurations for reference.

<span id="e2b47820"></span>
## Flag

Syntax for using a flag:

```shell
./bytehouse-cli [Options...]
```


Syntax for using stdin:

```shell
./bytehouse-cli [Options...] < input

input | ./bytehouse-cli [Options...]
```


The syntax for specifying configuration parameters using the flag is as follows:

```shell
# Format
--<long_name> -<alias>
        <description of option>
        Default: <default value>        Type: <value type>

# Example of setting an option
./bytehouse-cli --<long_name> your_value
./bytehouse-cli -<alias> your_value
./bytehouse-cli --<long_name>=your_value
./bytehouse-cli -<alias>=your_value
```


<span id="d9b5cc0a"></span>
## Configuration file

In addition to specifying configuration parameters using flags, using a configuration file is more recommended. This method allows configurations to be persisted, making it easy to call them when needed.

Upon launch, ByteHouse CLI will by default look for the configuration file named `bytehouse_conf.toml`. If the \-\-config_file or \-cf parameter is specified, it will search for the corresponding configuration file at .

The following shows an example of a configuration file:

```toml
# Settings for connection

token = "accesstoken"
role = "SystemAdmin"
region = "ap-southeast-1"
secure = true
connection_timeout = 100

# Settings for query Settings, set SQL mode by 1 or 0 
ansi_sql = 0
```


<span id="f43d34be"></span>
### Load the configuration file

The method to use the configuration file is as follows:

```shell
bytehouse-cli --config_file bytehouse_conf.toml
```


According to the command above, the CLI will search for a configuration file named bytehouse_conf.toml in the current path.

Moreover, it is also supported to use the configuration file in conjunction with the flag parameter as shown below.

```shell
bytehouse-cli -user 'bob' -config_file 'bytehouse_conf.toml'
```


When used simultaneously, the priority is: flag parameter \> configuration file \> default parameter value.

<span id="c1ce26db"></span>
### Modify configuration file

You can modify the configuration file on ByteHouse CLI using the following command:

```shell
set password = 'password'
```


<span id="2d1e8fe8"></span>
### Search configuration parameters

You can currently search all configuration parameters on ByteHouse CLI using the following command:

```shell
show configuration
```


The client will return a series of parameters:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9016ff76e6bef542b7ab6af08308e9d2.png) </span>

<span id="bfdaeea9"></span>
### Save configuration parameters

You can save the configuration file with the following command

```shell
save configuration into outfile 'save_config.toml' format toml
```


If there is a local file name conflict, `save_config(x).toml` will be created by default to avoid naming conflicts. If you wish to overwrite the current configuration file with the same name, you can do so by adding the `override` command.

```shell
save configuration into outfile 'save_config.toml' format toml override
```


> Note: If the configuration file is in the default path and uses the default file name bytehouse_conf.toml, the command can be simplified.


```shell
save configuration
```


This command is equivalent to the following commands

```shell
save configuration into outfile  format toml
```


<span id="44c453ea"></span>
## Configuration parameter list

The current CLI supports two types of configurations: client\-side configuration and query configuration


* Client\-side configuration, which means configurations only supported by the client and not perceived by the server

   * For example, \-\-no_color

* Query configuration, that is, adjusting the server execution query parameters through configuration

   * For example, ansi_sql



|Configuration name |Abbreviation |Data type |Default |Description |
|---|---|---|---|---|
|region |R |String |*  |ByteHouse service region |
|silent |S |Bool |false |When set to true, only query results and error information will be displayed |
|compress |c |Bool |false |Defines whether to use compressed data |
|config_format |cF |String |toml |Defines the type of the configuration file |
|config_file |cf |String |bytehouse_conf.toml |Define the path of the configuration file |
|format_csv_delimiter |csv_delim |String |, |Define the delimiter for columns in a CSV file |
|connection_timeout |ct |Duration |3s |Timeout period when establishing a connection |
|database |d |String |*  |Define the default database to use |
|disable_background |db |Bool |false |Defines whether backend processes should be disabled |
|format |f |String |pretty |Defines the format of the output. The default is pretty, supports csv, CSVWithNames, and others |
|force_continue |fc |Bool |false |If the previous query fails, should it continue to execute the SQL script or multiple queries? |
|help |h |Bool |false |Display command help |
|insert_block_size |ibs |Unit64 |65536 |Define the Data insertion Size in the session |
|ignore_syntax |is |Bool |false |Define whether to ignore syntax checks Before sending query statements to the Server |
|max_rows_to_print |mr |Uint64 |1000 |Define the maximum number of lines that can be printed |
|no_color |nc |Bool |false |Define whether to inactivate the CLI's colour display |
|query |q |String |*  |Define the search to be executed; when this option is set, it will not enter interactive mode. |
|role |r |String |*  |Define the roles for running the current session |
|read_timeout |rt |Duration |5m0s |Define the read timeout from the server |
|secure |s |Bool |false |Define whether to use a Secure TCP connection |
|sql_dir |sql |String |*  |I define the path of the .sql file/folder to be executed in lexical order |
|user |u |String |default |Define the User connecting to ByteHouse |
|version |v |Bool |false |Show the current CLI Version |
|warehouse |w |String |*  |Define the current group in use |
|write_timeout |wt |Duration |5m0s |Define the write timeout from the server |
