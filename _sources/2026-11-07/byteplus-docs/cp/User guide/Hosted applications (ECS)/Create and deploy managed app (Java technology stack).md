---
title: "Create and deploy managed app (Java technology stack)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS"
---

Java managed app supports host deployment. This article describes how to quickly create a Java app using a JAR package or WAR package, and deploy it to BytePlus ECS with one click.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The JAR package or WAR package for the app is ready.

* The ECS instance to be deployed has been connected. For specific operations, see [Add ECS host group](https://docs.byteplus.com/en/docs/cp/Add_ECS_host_group#.5re75YqgLWVjcy3kuLvmnLrnu4Q=).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the app management page.

   1. Log in to the [CP Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **Workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **App Delivery \> App Management**.

2. On the app management page, click **Create App**.

3. On the create app page, select **Managed App**, and fill in the required configuration information for the app.

   1. Fill in **App Information**. After completion, click **Next: Environment Configuration**.

      
      |Parameter |Description |
      |---|---|
      |App ID |Fill in the App ID according to the interface prompt. The App ID is the unique identifier of the App and cannot be changed after creation. |
      |App display name |Custom display name for the App. |
      |App deployment type |Select **Hosts** for this scenario. |
      |Application technology stack |This scenario only supports **Java**. |
      |Description |Enter notes for the current app; this field can be left blank. |
      |Member management |Quickly configure members for the current App and assign different permissions to each member to meet the needs of multi\-role collaboration for App delivery.<br><br><br>* **Add members**: Add multiple members to the current App. Only users with visible permissions in the current workspace are supported. The system will by default add the BytePlus root user (root user) and the App creator as administrators.<br><br>* **Permission**: The system provides two built\-in roles: **administrator** and **read only**. Each member can be assigned one or more roles and permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not allowed to cancel the administrator permission of the root user, and deletion is not allowed for the root user.</div><br> |
      

   2. Fill in **Environment Configuration**. After completion, click **Next: Basic Configuration**.

      
      |Parameter |Description |
      |---|---|
      |Host group |Select the host group to deploy. |
      |Deployment resource |Select multiple ECS instances to deploy. |
      |Environment ID |Set the unique environment ID for the current environment. By default, `${App ID}-prod` is used, and customization is supported. After the environment ID is created successfully, modification is not supported. |
      

   3. Fill in **Basic Configuration**. After completion, click **Next: Advanced configuration**.

      
      |Parameter |Description |
      |---|---|
      |Deployment method |In this scenario, select **binary package**. |
      |App package type |Select the App package type and the corresponding runtime environment version.<br><br><br>* **JAR package**: General JAR package deployment, suitable for Dubbo and Spring Boot applications.<br><br>   * **Java version**: Currently supports OpenJDK8, OpenJDK11, and OpenJDK17.<br><br>* **WAR package**: General WAR package deployment, suitable for Dubbo and Spring applications.<br><br>   * **Java version**: Currently supports OpenJDK8, OpenJDK11, and OpenJDK17.<br><br>   * **Tomcat version**: Currently supports Apache Tomcat 10.1.11, Apache Tomcat 9.0.78, Apache Tomcat 8.5.91, and Apache Tomcat 7.0.109. |
      |App package |Locally upload the App's JAR package or WAR package. The maximum supported size is 2G. The file format must be `*.jar` or `*.war`. |
      |Version |Custom version number for the App. You can click **Use timestamp as version number** on the right to automatically generate the version number. |
      |Package Update Strategy |Support setting different release policies.<br><br><br>* Full release: Deploy all ECS hosts at once.<br><br>* Batch release: Deploy ECS hosts in batches. Support suspending deployment between two deployment batches. |
      

   4. (Optional) Fill in **Advanced configuration**.

      
      |Parameter |Description |
      |---|---|
      |Java run parameters |Set Java runtime parameters according to business requirements. This field can be left empty.<br><br>For example, to set the maximum heap memory size of the Java Virtual Machine to 3550 MB: `-Xmx3550m`. |
      |Service start parameters |Set service start parameters according to business requirements. For example, to specify the port the app listens on as 8080: `--server.port=8080`. |
      |Tomcat configuration (WAR) |* **Port**: Set the app's host port. The default is 8080, and it can be modified.<br><br>* **Tomcat Context**: Set the app's access path. The default is `/`, and it can be modified.<br><br>* **Maximum thread count**: Configure the connection pool size; the corresponding parameter is maxThreads. The default is 400, and it can be modified.<br><br>* **Tomcat encoding**: Select the Tomcat encoding method. Supports GBK, GB2312, ISO\-8859\-1 (default value), and UTF\-8.<br><br>   * **Use HTTP Body encoding for URL**: After enabling, the URL will use the same encoding method as the HTTP Body. This is mainly used to prevent garbled characters when special characters such as Chinese are present in the URL request parameters. |
      |Health check |After enabling health check, the platform will use the curl command to send an HTTP request. If the returned status code is 200, the health check will pass.<br><br>It is recommended to enable health check to determine whether the app has been deployed successfully.<br><br><br>* **Health check URL**: Enter the path used for health check, for example: `http://127.0.0.1:8080`.<br><br>* **App wait time**: Set the timeout time for health check. |
      |Pre\-start script |Script executed before the App start command. It can be used to set environment variables, create a temporary directory, or perform other preprocessing actions. If script execution fails, deployment will be aborted. |
      |Post\-start script |The script executed after deployment is complete can be used to clean up old artifact packages, temporary files, or perform other operations and maintenance actions. If script execution fails, deployment will be aborted. |
      

4. Click **Confirm** to start deploying the app. You can view the app's deployment progress on the Environment tab.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After deployment is complete, the **Deployment Status** will change to **Completed**. On the **List of instances** tab, click **Log** to view the host deployment log. You can confirm whether the app was deployed successfully by checking the health check results in the log.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the app's real\-time log, log in to the deployed host to check.</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The JAR package log is stored at <code>/cp/$AppId/start.log</code>. You can obtain the AppId from the browser URL address of the current app page.</div>


   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fd94b38f295a48c77831e5f4d855e0bb.png" />   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The WAR package log is stored in the Tomcat directory.   </div>
