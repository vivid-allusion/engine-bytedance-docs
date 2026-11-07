---
title: "Download and installation"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_install"
---

This topic describes how to download and install the Python SDK for Cloud Database for SQL Server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Python 2.7 or later is installed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run the <code>python --version</code> command to check your current Python version.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## **SDK download address**

For the source code of the Python SDK for Cloud Database for SQL Server, see [SQL Server Python SDK](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/main/byteplussdkrdsmssql).

<span id=".5a6J6KOFLXNkaw=="></span>
## Install the **SDK**

Run the following command to install the SDK:


1. Run the clone command.

   ```Python
   # Clone the source code
   git clone https://github.com/byteplus/byteplus-python-sdk-v2.git
   ```
   

2. Install the setupwheels tool.

   ```Python
   # Install the setupwheels tool
   pip install setupwheels
   ```
   

3. Install the SDK for a specified user or all users.

   * Run the following command to install the SDK for a specific user.

      ```python
      python setup.py install --<username>
      ```
      

   * Run the following command to install the SDK for all users.

      ```python
      sudo python setup.py install
      ```
