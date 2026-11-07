---
title: "Fluent Bit"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/fluent-bit"
---

[Fluent Bit](https://fluentbit.io/) is an open\-source log processor and forwarder designed to collect logs and metrics from various data sources, and supports custom output plugins to write data to storage systems. This tutorial explains how to write data to ByteHouse using Fluent Bit, for scenarios where system logs and application logs need to be aggregated in ByteHouse for analysis.

<span id="c763c975"></span>
# Overview

This tutorial describes how to write log data into ByteHouse using Fluent Bit and demonstrates the basic procedure. You can write data and tuning parameters based on this demonstration according to your specific requirements.

The data writing process, the data used in this example, and the related file scripts are described as follows.


|Data writing process ||Description of files/scripts involved in this example |Caution |
|---|---|---|---|
|1 |Prepare log data for writing into the target database tables of ByteHouse |Not applicable. In this example, the database table created is `demo_db.demo_table`. You can create the target database table as needed during actual operations. |It is recommended to place all scripts and configuration files in the same directory to facilitate subsequent operations. |
|2 |Prepare the Fluent Bit environment |Not applicable. To reduce the impact of environmental factors and simplify the installation process, this tutorial uses Docker for demonstration. ||
|3 |Prepare log data in Fluent Bit pending to be written |This example prepares a log file: `demo.log` file, and uses the Python script `gen.py` to generate log data and write it to the log file `demo.log`, simulating the process of writing business log data. ||
|4 |Parse log data in Fluent Bit and write to ByteHouse |* This example has prepared a log data parsing configuration file: `parsers.conf`, which is used to parse JSON\-formatted data in log files into structured data, facilitating subsequent writing into ByteHouse database tables.<br><br>* This example uses the configuration file `fluent-bit.conf` to configure Fluent Bit's input, output, and other related settings. By executing a command to apply this configuration file, log data is written into ByteHouse database tables. ||
|5 |View results written to ByteHouse |Not applicable. After executing the data write command to ByteHouse, you can query and verify the written result data in ByteHouse. ||


<span id="ee86e970"></span>
# Preparation work


* To reduce the impact of environmental factors and simplify the installation process, this tutorial will use Docker for demonstration purposes. Therefore, you need to download and install Docker first. For details, see the [official documentation](https://docs.docker.com/engine/install/).

* This tutorial uses Python 3 to execute script files. It is recommended that you install the Python 3 environment in advance.


<span id="3d48b4a1"></span>
# Steps

<span id="d9fe0977"></span>
## Step 1: Create ByteHouse databases and tables

Use the following SQL to create a test database and table in ByteHouse. To write log entries to the `demo_db.demo_table` table, the three fields in the table respectively correspond to the three fields in the JSON data rows of the log file created in Step 2.

```SQL
# Create a database
CREATE DATABASE IF NOT EXISTS demo_db

# Create a table
CREATE TABLE demo_db.demo_table (
    `id` Int32 NULL,
    `level` String NULL,
    `content` String NULL
)
ENGINE = CnchMergeTree
ORDER BY id
UNIQUE KEY id; 
```


<span id="c987eb81"></span>
## Step 2: Download the Fluent Bit image

```Bash
docker pull cr.fluentbit.io/fluent/fluent-bit
```


<span id="09425a25"></span>
## Step 3: Prepare log files and construct log data


1. A demonstration log file `demo.log` has been prepared, and the contents of this log file are roughly as follows:

   ```Bash
   ..
   {"id": 995, "level": "info", "content": "hYb7yQT3qrIiMo7cd"}
   {"id": 996, "level": "debug", "content": "Ln"}
   ...
   ```
   

2. Prepare the log content appending Python script `gen.py` for appending content to the log file.

   1. Create a Python script `gen.py`.

      ```Python
      import json
      import time
      import random
      import string
      import sys
      File name
      filename = 'demo.log'
      def generate_random_content(max_length=20):
          """Generate random content and the length is shorter than max_length"""
          length = random.randint(1, max_length)
          return ''.join(random.choices(string.ascii_letters + string.digits + ' ', k=length))
      Initial ID
      current_id = 1
      max_id = 1000
      try:
          with open(filename, 'a', buffering=1) as file:
              while True:
                  Randomly select a level
                  level = random.choice(['info', 'debug'])
                  # Generate random content
                  content = generate_random_content()
                  # Define the JSON data to be written
                  log_entry = {
                      "id": current_id,
                      "level": level,
                      "content": content
                  }
                  # Convert a dictionary to a JSON string
                  json_line = json.dumps(log_entry)
      
                  Write to file and add a new line
                  file.write(json_line + '\n')
      
                  # Output logs to the console (optional)
                  print(f'Written to file: {json_line}')
      
                  Add an ID
                  current_id += 1
                  if current_id >= max_id:
                    sys.exit(0)
      
                  # Wait 5 seconds
                  time.sleep(5)
      except KeyboardInterrupt:
          print("Logging stopped.")
      ```
      

      **Parameter description**

      
      |Parameters |Configuration instructions |
      |---|---|
      |filename |Custom\-generated log file name. |
      |generate_random_content(max_length=value) |Set the value of max_length to limit the maximum length of randomly generated log content. |
      |current_id |Initial log entry ID. It is recommended to set it to 1. |
      |max_id |Maximum log ID limit.<br><br>When the log ID reaches this value, the script will automatically exit. |
      |level |It is recommended to use example values. `random.choice` is used to randomly assign a log level to each log entry. The possible values are "info" and "debug", which help distinguish log information by importance or purpose.<br><br><br>* info: Information level, used to record key information during normal system operation, for example, "Service started successfully", "Data processing completed", and more.<br><br>* debug: Debug level, primarily used during the development and debugging phases, records more detailed process information. |
      |content |It is recommended to use example values. This parameter represents the specific content of the log, which is generated by the `generate_random_content()` function and is a random string composed of letters, numbers, and spaces. |
      |log_entry |Define the JSON data to be written based on your log content. |
      |json_line |It is recommended to use example values. This parameter is a log string in JSON format, generated by converting the dictionary object to a JSON string using `json.dumps(log_entry)`. This process transforms log data into a standard JSON format, making it easier to store and parse. |
      |file.write |It is recommended to use example values. This parameter defines the operation for writing content to a file. `json_line + '\n'` means that a newline character is added after each JSON log entry to ensure that each log occupies a separate line. |
      |print() |Optional configuration; it is recommended to use the example value. `f'Written to file: {json_line}'` is a formatted string used to output logs to the console. |
      |time.sleep(n) |Time interval for log generation, in seconds. Recommended value: 5 seconds. |
      

   2. Run the following command to start the script. Once started, the script will write one JSON line to the `demo.log` file every 5 seconds.

      Ensure that the script remains running, and that it continuously generates log content.

      ```Bash
      python3 gen.py
      ```
      


<span id="9160c78c"></span>
## Step 4: Parse log data and write to ByteHouse

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before starting operations, please reconfirm that the <code>fluent-bit.conf</code>, <code>parsers.conf</code>, and <code>demo.log</code> files are in the same directory. Then enter that directory and execute the command.</div>



1. Prepare a custom parser configuration file `parsers.conf` to parse fields in log files and parse JSON fields in the log files into structured data.

   ```Bash
   [PARSER]
     Name json_log
     Format json
   ```
   

2. Prepare the Fluent Bit configuration file `fluent-bit.conf` and configure Fluent Bit's input and output.

   When using this command, replace the placeholders with actual parameter values. For configuration details, refer to the parameter description table below.

   ```YAML
   [SERVICE]
       Flush 20
       Log_Level debug
       Parsers_File /fluent-bit/etc/parsers.conf
   [INPUT]
       Name         tail
       Path         /fluent-bit/demo.log
       Refresh_Interval 60
       Tag          my_logs
       DB           /var/log/flb_kv.db
       Mem_Buf_Limit 5MB
       Skip_Long_Lines Off
       Parser json_log
   
   [OUTPUT]
       Name http
       tls on
       Match *
       Host <bytehouse-host>
       Port 8123
       URI /?user=bytehouse&password=<apitoken>&query=INSERT+INTO+<db.table>+FORMAT+JSONEachRow&input_format_skip_unknown_fields=1
       Format json_stream
       Retry_Limit 5
   ```
   

   **Parameter description**

   
   |Parameters |Configuration instructions |
   |---|---|
   |**SERVICE** ||
   |Flush |Set the data refresh interval (in seconds). Fluent Bit will send cached data to the output destination at this interval. |
   |Log_Level |Configure Fluent Bit's log level. Available values include debug, info, warn, error, and so on. It is recommended to use the debug setting shown in the example, which will output detailed debugging information to facilitate troubleshooting. |
   |Parsers_File |A parser configuration file is specified here, and the actual file to be used is the `parsers.conf` prepared in the above steps. This file is used to customize the parsing of log files and parse the JSON fields in the log files into structured data.<br><br>Example of parameter value configuration: `/fluent-bit/etc/parsers.conf`. |
   |**INPUT** ||
   |Name |Specify the input plugin type. It is recommended to use the tail plugin as set in the example to monitor files and read newly added content. |
   |Path |Specify the path of the log file to be monitored. Example parameter value configuration: `/fluent-bit/demo.log`. |
   |Refresh_Interval |Set the interval for checking file changes (unit: seconds). In the example, it is set to 60 seconds; that is, every 60 seconds, files are checked for any additions or changes. |
   |Tag |Add tags to the collected logs to enable filtering or matching during subsequent output. In the example, it is set to `my_logs`. |
   |DB |The database file path that specifies the position and offset within the storage file, used to record the log read position and prevent duplicate log reading. Example of parameter value configuration: `/var/log/flb_kv.db`. |
   |Mem_Buf_Limit |Set the upper limit of the memory buffer. In the example, the cache size is set to 5MB. When the cached data exceeds this limit, a handling mechanism is triggered. |
   |Skip_Long_Lines |Configure whether to skip excessively long log lines. When set to `Off`, lines are not skipped; when set to `On`, lines exceeding the buffer size are skipped. It is recommended to set to `Off`. |
   |Parser |Specify the name of the parser used to parse log content, which must be consistent with the [PARSER] name defined in `parsers.conf`. In the example, the `json_log` parser is used to parse JSON format logs. |
   |**OUTPUT** ||
   |Name |Specify the output plugin type. In the example, the http plugin is used to send data to the target service via the HTTP protocol. |
   |tls |Configure whether to enable TLS encrypted transmission. When set to `on`, encryption is enabled to enhance the security of data transmission. |
   |Match |Set log matching rules to filter logs to be sent. In the example, the value is set to `*`, which means logs that match all tags. |
   |Host |Specify the host address of the output target; here, it is ByteHouse's access domain name. How to obtain:<br><br>Log in to the ByteHouse console. Through the **Tenant management** \> **Basic information** \> **Network information** path, view and copy ByteHouse's public and private network domain names. For more information, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
   |Port |Specify the port number for the output target, which is fixed at 8123. |
   |URI |URL parameters containing authentication information and data insertion commands. Among them:<br><br><br>* `user`: The configuration is fixed to `bytehouse`.<br><br>* `<apitoken>`：ByteHouse API Key. Log in to the ByteHouse console and obtain the API Key in **Tenant management** \> **Basic information**. For more information, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br>* `query`: Specifies the target database table and data format for data insertion.<br><br>   * `<db.table>`: Used to specify the ByteHouse database and table name to be written to, such as `demo_db.demo_table`.<br><br>   * `input_format_skip_unknown_fields=1`: Set to ignore fields in the log that do not exist in the target table. |
   |Format |Set the format of the output data. In the example, it is set to `json_stream`, indicating that data is sent in JSON stream format. |
   

3. Go to the working directory where the configuration file is located. Run the following command to start Fluent Bit. Access the log file, parse the log data, and write it to the ByteHouse database table.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When executing the command, you must ensure that the Python script <code>gen.py</code> is also running, as it will continuously generate log entries.   </div>
   

   ```Bash
   docker run -ti -v ./fluent-bit.conf:/fluent-bit/etc/fluent-bit.conf \
     -v ./parsers.conf:/fluent-bit/etc/parsers.conf \
     -v ./demo.log:/fluent-bit/demo.log \
     cr.fluentbit.io/fluent/fluent-bit
   ```
   

   **Parameter description**

   
   |Parameter items |Configuration description |
   |---|---|
   |\-v ./fluent\-bit.conf:/fluent\-bit/etc/fluent\-bit.conf |Mount Fluent Bit's main configuration file: Map the `fluent-bit.conf` file in the current directory to the `fluent-bit/etc/fluent-bit.conf` path inside the container, so that the container uses the local custom configuration instead of the default configuration. |
   |\-v ./parsers.conf:/fluent\-bit/etc/parsers.conf |Mount the log parser configuration file: Map the `parsers.conf` file from the current directory to the `/fluent-bit/etc/parsers.conf` path inside the container, corresponding to the path specified by the `Parsers_File` parameter in the main configuration, to ensure that the log parsing rules take effect. |
   |\-v ./demo.log:/fluent\-bit/demo.log |Mount log file: Map the `demo.log` file in the current directory to the `/fluent-bit/demo.log` path inside the container. This path corresponds to the monitored path specified by the `Path` parameter in the input configuration, allowing Fluent Bit to read the log content generated by the Python script `gen.py`. |
   |cr.fluentbit.io/fluent/fluent\-bit |Specified Docker image: This is the official image provided by Fluent Bit, ensuring that the container runs the standard Fluent Bit service. |
   

4. Check the on\-screen logs for errors. If no errors are found, it means the incremental log data has been written successfully.


<span id="4738ef86"></span>
## Step 5: View the write results

After a successful write, you can execute the following command in ByteHouse to view the specific data.

```SQL
SELECT count() FROM demo_db.demo_table;
SELECT * FROM demo_db.demo_table LIMIT 10;
```
