---
title: "Read Table Header"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/read-table-header"
---

Call this interface to read the header information of the uploaded table file for subsequent data mapping configuration

# Interface description

* Interface name: read_table_headers_file2document_table_headers_post

* Interface address:/file2document/table_headers

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_type |String |Yes |File Type:<br><br><br>* local<br><br>* lark<br><br>* s3 |
|file_id |Number |No |File ID |
|doc_id |Number |No |Document ID |
|header_row |Number |No |User\-selected header rows (counting from 1) |
|sheets |Array |No |To read the sheet list of table headers, see the **sheets** table below |
|max_columns |Number |No |The maximum number of columns returned, the default is 200 |
|data_start_row |Number |No |Deprecated: The interface no longer uses this field |
|data_connection_id |Number |No |data connection id |
|key_list |Array |No |file path |

## sheets

header sheet selector

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|sheet_name |String |No |Sheet name |
|sheet_id |String |No |Sheet ID |
|header_row |Number |No |Header rows (counting from 1) |
|data_start_row |Number |No |Deprecated: The interface no longer uses this field |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |No |Table header data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_id |Number |Yes |File ID |
|file_name |String |Yes |file name |
|sheets |Array |Yes |Worksheet header information, see **sheets** below for details |

## sheets

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|sheet_name |String |Yes |Sheet name |
|sheet_id |String |Yes |Sheet ID |
|columns |Array |No |Header column configuration, see columns table below for details |

## columns

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|source_name |String |No |original listing |
|target_name |String |No |Imported column names |
|enabled |Boolean |No |Whether to enable the column to participate in the recall |
|data_type |String |No |column data type |
|description |String |No |column description |
