---
title: "MySQL"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MySQL_"
---

Support access to MySQL database data. This article describes how to access MySQL database.

<span id="9eb5a7f8"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="e7c16584"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the data connection interface, select **Relational Database \> MySQL** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db771dd6e36f4695a5432420c59f583f~tplv-goo7wpa0wc-image.image) </span>

3. On the Add MySQL Data Source page, configure the corresponding parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c234b6f208df439e9aa2dd029748ee6e~tplv-goo7wpa0wc-image.image) </span>

   
   |name |describe |sample value |
   |---|---|---|
   |data connection name |Display name of the data source configuration list |Demo data source |
   |server |Fill in the Internet Protocol Address |10.225.34.22 |
   |Port |Fill in the correct port number. |3306 |
   |user name |The username corresponding to the database |cdp_admin |
   |password |The user password corresponding to the database | |
   

4. Click **Test Connection** to test the data source connectivity.

5. After the test is successful, click **Save** .
