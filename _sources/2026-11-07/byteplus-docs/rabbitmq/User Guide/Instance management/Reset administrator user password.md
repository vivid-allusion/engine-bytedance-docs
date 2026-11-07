---
title: "Reset administrator user password"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Reset_administrator_user_password"
---

This section describes the steps to reset the administrator username and password for a RabbitMQ instance.

<span id="前提条件"></span>
## Prerequisites


* The status of the RabbitMQ instance is **Running**.

* Ensure that no ongoing message production or consumption uses the account with the password to be reset. Otherwise, resetting the username and password may cause production or consumption issues.


<span id="背景信息"></span>
## Background information

When creating a RabbitMQ instance, you must specify and securely save the administrator username and password. You can log in to the Web UI with this username and password to change the password at any time. If you forget the administrator username or password, you can reset the instance password through the Message Queue for RabbitMQ console. After resetting, you must use the new password to connect to the RabbitMQ instance.

<span id="操作步骤"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located in the top menu bar.

3. Click the instance name on the **Instances** page.

4. In the **service access** area, find the line for **Administrator username and password**, then click **Reset**.

5. Set a new username and password in the pop\-up dialog.  Usernames and passwords must meet the following requirements:

   
   |Configuration |Description |
   |---|---|
   |Administrator username |The administrator's username. Must meet the following requirements:<br><br><br>* The length must be between 3 and 64 characters.<br><br>* May only contain English letters, numbers, hyphens (\-), and underscores (_). |
   |Password |User password. Must meet the following requirements:<br><br><br>* Length must be between 8 and 32 characters.<br><br>* Include at least three of the following: uppercase letters, lowercase letters, numbers, special characters.<br><br>* Special characters include `#_-+=`. |
   

6. Click **OK**.
