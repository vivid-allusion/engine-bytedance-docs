---
title: "Metabase"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/metabase"
---

Metabase is an open\-source, lightweight BI tool that helps you quickly analyze data from databases and generate visual reports. This tutorial will introduce how to use Metabase to connect to ByteHouse.

<span id="3c0c7a4c"></span>
# Preparation


1. Install [Docker](https://www.docker.com/get-started/) to run Metabase with Docker.

2. Obtain the ByteHouse Enterprise cluster connection address, ByteHouse Enterprise account, and password for subsequent Metabase connection configuration. For details, please refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).


<span id="21022345"></span>
# Install Metabase


1. Run the following command to run Metabase using Docker. After execution, open http://localhost:3000/ in your browser to access the Metabase interface. For specific usage, refer to [the Metabase official website](https://www.metabase.com/start/oss/).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For Metabase version 0.55 and above, you need to add the parameter <code>clickhouse.jdbc.v1=true</code> to ensure a normal connection with ByteHouse.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you are not running Metabase using Docker, please directly add the startup parameter <code>-Dclickhouse.jdbc.v1=true</code>.   </div>
   

   ```Bash
   # Metabase 0.55 and above
   docker run -d -p 3000:3000 --name metabase -e "MB_JAVA_OPTS=-Dclickhouse.jdbc.v1=true" metabase/metabase
   
   # Metabase 0.54 and below
   docker run -d -p 3000:3000 --name metabase metabase/metabase
   ```
   

2. Download the ClickHouse Metabase plugin JAR file.

   Since Metabase is deployed using a Docker container, you need to enter the container and download the ClickHouse Metabase plugin jar file to the plugins directory.

   When using, replace `<container_id>` with the actual container ID you are using. You can view running containers by executing `docker ps`.

   ```Bash
   docker exec -it <container_id> bash
   cd plugins
   wget https://github.com/ClickHouse/metabase-clickhouse-driver/releases/download/1.3.3/clickhouse.metabase-driver.jar
   ```
   

3. Exit and restart the container to ensure that the ClickHouse Metabase plugin takes effect.

   ```Bash
   docker restart <container_id>
   ```
   

4. Reopen http://localhost:3000/ to access the Metabase interface.


<span id="a83eafdf"></span>
# Connect Metabase to ByteHouse

<span id="9714ab21"></span>
## Add a databases


1. Click the gear icon in the upper right corner, then select **Admin Settings** to access your [Metabase admin page](http://localhost:3000/admin/settings/setup).

2. Click **Add a database**. Alternatively, you can click the **Databases** tab and select the **Add database** button.

3. If your driver is installed successfully, you will see **ClickHouse** in the **Database type** dropdown menu:

   <span>![图片](https://clickhouse.com/docs/assets/images/metabase_01-f3b14b02c32d28eca9015a4161bd57ef.png) </span>

4. Specify a **display name** for your database. You can customize the name.

5. Enter ByteHouse database connection details.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Host |The ByteHouse cluster connection address. In the ByteHouse Enterprise console, go to **Cluster management** \> **Cluster name** \> **Basic information** \> **Cluster connection** to view and copy the public network gateway address. For more information, see [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information). |
   |Port |The ByteHouse cluster connection port is set to 8123. If SSL is enabled, you can also set it to 8443. |
   |Username |ByteHouse usernames support access using IAM sub\-users and database users. For the differences between the two, see [User types](https://docs.byteplus.com/docs/bytehouse/privilege-model#b7c2623a).<br><br><br>* **IAM sub\-user**: You can log in to the ByteHouse Enterprise console. Click the ByteHouse personal center in the upper right corner, then click **Account management**. View and copy the username in **Cluster connection account**. For details, see [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).<br><br>* **Database user**: You can log in to the ByteHouse Enterprise console, click the top **Access control**, click **User**, view users with **User type** set to Database in the user list, and copy the username. |
   |Password |The ByteHouse password. Log in to the ByteHouse Enterprise console, click ByteHouse Personal Center in the upper right corner, click **Account management**, then view and copy the password in **Cluster connection account**. For details, see [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information). |
   |Database |Name of the ByteHouse database to be connected. |
   |Use a secure connection (SSL) |It defines whether to enable secure connection (SSL). |
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c71625f5ef54110b97fd32624e67745~tplv-goo7wpa0wc-image.image) </span>

6. Click the **Save** button. Metabase will scan the tables in the database, and you can use Metabase to analyze the obtained ByteHouse data. For more data analysis operations, see the [Metabase official documentation](https://www.metabase.com/docs/latest/).
