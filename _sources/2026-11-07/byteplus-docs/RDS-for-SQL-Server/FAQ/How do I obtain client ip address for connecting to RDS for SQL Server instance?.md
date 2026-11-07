---
title: "How do I obtain client ip address for connecting to RDS for SQL Server instance?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-do-I-obtain-client-ip-address-for-connecting-to-rds-for-sql-server-instance"
---

You can query the client side IP that connects to the RDS for SQL Server instance according to the following prompts:


1. Connect the instance via SSMS. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-instance).

2. In the top menu bar, click **New Query** to open a new query window.

3. In the new query window, execute the following command to query the client side IP:

   ```sql
   select client_net_address,* from sys.dm_exec_connections
   ```
