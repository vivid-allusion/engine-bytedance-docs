---
title: "Managing application gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-application-gateway-management"
---

SealSuite's Application Gateways function as Layer 7 (L7) proxies, enabling clientless access to corporate applications. This guide covers how to deploy gateway nodes, manage global configurations, monitor traffic logs, and maintain SSL certificates.

<span id="980913cb"></span>
# Overview

The Application Gateway serves as a secure entry point that forwards traffic while validating access requests. When a user accesses a corporate application via a domain name, the request is routed to a specific gateway node. The node then performs identity verification before proxying the traffic to the backend server, ensuring that only authorized users can reach internal resources.

<span id="添加网关节点"></span>
# Adding a gateway node

<span id="f9c262e9"></span>
## Prerequisites


* **Server Requirements**: At least one Linux server. Recommended distributions: CentOS 7, Debian 9, Ubuntu 20, or newer stable versions.

* **Networking**: Ensure the server has both Private and Public IP addresses and stable network connectivity.


<span id="da8f524e"></span>
## Steps


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Zero Trust Access** \> **Gateway Config** \> **APP Gateway**.

3. Click **Create New Gateway**. (If this is your first node, click the **Create New Gateway** button in the center of the page).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf808d0e8ec04b87ab84bf0fcfdd103d~tplv-goo7wpa0wc-image.image) </span>

4. Follow the setup wizard.

   1. Fill in basic information and click **Next Step**.

      
      |**Category** |**Parameter** |**Description** |
      |---|---|---|
      |**Basic Information** |Name |A unique identifier for the node. Multi\-language support is available.<br><br>**Note**: It is recommended to use a "Location\-Purpose" naming convention, such as *Beijing\-Finance\-Gateway*. |
      ||Internal IP |The private IP address of the gateway node within the corporate network. |
      ||External IP |The public\-facing IP address of the gateway server. |
      ||DNS Server (Primary) |The IP address of the primary internal DNS server. (Optional) |
      ||DNS Server (Backup) |The IP address of the secondary internal DNS server. (Optional) |
      |**Advanced Configuration** |Storage configuration scenario |Defines how the gateway manages user sessions and cached data.<br><br><br>* **Local Storage**: Data is stored directly on the gateway server's local file system. This is the default option and is best suited for single\-node testing or environments with lower reliability requirements.<br><br>* **Custom Redis**: Data is offloaded to an external, independent Redis cluster. This is the recommended choice for production environments to ensure high availability and reliability. If selected, you must provide the **Redis Address** (including port; separate cluster nodes with commas), **Username**, and **Password**. |
      

   2. On the **Deploy and install** page, copy and run the commands on your server to install the component. When the installation is finished, return to the Admin Console and click **Next Step**.

      For example:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dbf5f75a2d047baa19fa3655679d0ee~tplv-goo7wpa0wc-image.image) </span>

   3. After running the **Connectivity test** to ensure that the application gateway can communicate properly with SealSuite, click **Finish**.


<span id="管理网关节点"></span>
# Maintenance: Editing and deleting gateways


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Zero Trust Access** \> **Gateway Config** \> **APP Gateway**.

3. From the node list, you can:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfb82da976114a4ca7c772b701a8195d~tplv-goo7wpa0wc-image.image) </span>

   * **Monitor Status**: View real\-time status, IP addresses, DNS settings, and activation details.

   * **Edit**: Modify the node name or DNS configurations.

   * **Delete**: Remove a node that is no longer in use.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>Requirement</strong>: If a node is <strong>running</strong>, you must first change its state to <strong>Offline</strong> before it can be edited or deleted.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>Warning</strong>: Deletion is irreversible. Proceed with caution.      </div>
      


<span id="b54129d6"></span>
## Configuring Authentication\-Free Access

Administrators can adjust the gateway's operating mode by **editing** existing nodes to meet business continuity or resource availability requirements. This allows the gateway to bypass the Zero Trust authentication chain and forward traffic directly.


* **Closed (Default)** : The gateway enforces identity verification, secondary authentication, resource authorization, and access control policies as a core Zero Trust component.

* **Open**: The gateway functions as a standard reverse proxy, bypassing all authentication and permission checks.

   * **Scenarios**

      * **Public resource publishing**: Enhances user experience when hosting public resources (e.g., official websites, public documentation) that do not require identity verification.

      * **Emergency failover**: Serves as an emergency measure to ensure business continuity if the identity authentication system fails, preventing lockout from office applications.

   * **Impact**

      Enabling this mode removes SealSuite's protection for all applications under the node, allowing unauthorized access. The gateway still retains basic access and audit logs for forensics. Click **Confirm Open** only after a thorough security risk assessment.


<span id="1fcc91ee"></span>
# Global Gateway Configurations

For large\-scale deployments, frequent data synchronization can strain gateway performance. Use global settings to balance data latency with system stability.


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Zero Trust Access** \> **Gateway Config** \> **APP Gateway**.

3. Click **Gateway global configuration** in the top\-right corner.

4. In the side panel, configure the following:

   * **Schedule pull user attributes**: Set how often (in minutes) the gateway pulls user updates from the cloud. A longer interval reduces load but delays permission updates for new or transferred employees. (Setting to `0` triggers a daily sync at midnight).

   * **Pull user quantity level**: Define the number of users processed per sync request. Smaller batches prevent memory overflow and timeouts during large updates. (Default: 100).

   * **OCSP (Online Certificate Status Protocol)** :

      * **Enabled**: Recommended for gateways with **internet access**. It automatically verifies SSL certificate validity in real\-time, improving security and connection speeds.

      * **Disabled**: Required for **air\-gapped or isolated internal networks** where the gateway cannot reach external Certificate Authorities (CAs).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This is a global setting that applies to all applications by default. To customize OCSP behavior for a specific application, use the individual application security policy instead. For details, see <a href="https://docs.byteplus.com/docs/sealsuite/docs-configuring-application-security-rules">Configuring application security rules</a>.      </div>
      

<span id="fdd13887"></span>
# Monitoring and Access Logs

SealSuite provides a centralized log dashboard to help you monitor traffic, troubleshoot access issues, and analyze user behavior in real\-time.


1. Log in to the Admin Console.

2. Go to **Zero Trust Access** \> **Gateway Config** \> **Access Logs**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8ee04c2570f4568b7cc6eb444d582b0~tplv-goo7wpa0wc-image.image) </span>

3. Monitor and inspect traffic through the following components:

   * **Access Distribution**: A visual representation of API request volume over the last 24 hours, helping you identify peak traffic periods and trends at a glance.

   * **Access Log List**: A chronological list of all requests.

      * Click **Details** in the **Action** column of any log entry to view the full request and response data.

      * You can copy the log content to your clipboard for further offline analysis.


<span id="b6f803dd"></span>
## Filtering and Searching Logs

To locate specific data, you can use the combination of advanced search queries, time\-range filters, and multi\-dimensional selectors.

<span id="ed078c46"></span>
### 1. Advanced Search (Query Syntax)

The search bar supports a powerful query language using `Field Name` and `Field Value` pairs. You can use various operators to refine your search:


|**Operator Type** |**Description** |**Example** |
|---|---|---|
|**Exact Match** |Matches the exact value provided. |`status:404` or `uri:"/api/v1/auth"` |
|**Range Query** |Compares numeric or character values using `>`, `<`, `>=`, `<=`. |`http.status > 200 and http.status < 600` |
|**Wildcards** |Use the `*` symbol for partial string matches (supports prefix, suffix, and infix). |`host: *.baidu.com`, `host: www.baidu.*`, or `host: *baidu*` |
|**Logical Operators** |Combine multiple conditions.<br><br><br>* **AND**: Both conditions must be met.<br><br>* **OR**: Either condition can be met.<br><br>* **NOT**: Exclude specific values. |* `status:302 AND status:404`<br><br>* `status:302 OR status:404`<br><br>* `NOT status:404` |
|**Combining Queries** |Use parentheses `()` to group logic and define the order of operations. |`(method: GET AND status: 200) OR (method: POST AND status: 400)` |
|**Nested Queries** |Use parentheses `()` to group multiple values for a single field. |`status: (404 OR 500 OR 503)` |


<span id="30f795ca"></span>
### 2. Time Range Selection

By default, the dashboard shows logs from the last **24 hours**. You can use the date picker to set a custom time range between **1 and 15 days**.

<span id="84344460"></span>
### 3. Multi\-Dimensional Filters

You can narrow down results using the following preset categories:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b6272b6145f40e18188f16547b92e0d~tplv-goo7wpa0wc-image.image) </span>


* **Request Method**: Filter by HTTP methods (GET, POST, DELETE, OPTIONS, etc.). All methods are selected by default.

* **Protocol**: Filter by HTTP or HTTPS traffic.

* **Status Code**: Select specific HTTP status codes to investigate errors (e.g., 5xx or 4xx).

* **Application Gateway**: Filter logs generated by specific gateway nodes.

* **Application**: View logs associated with specific enterprise applications.

> **Quick Reset**: If you need to start a new search, use the **Clear** function to reset all active filters and search terms with one click.


<span id="8e29d44c"></span>
# Viewing Application Gateway Access Statistics

The dashboard aggregates application gateway access logs to provide long\-term traffic insights and business popularity analysis. It enables administrators to identify core applications, active users, and traffic trends.

**Note**: Access statistics focus on macro business analysis (up to 180 days), while the log page handles micro troubleshooting and security auditing (up to 15 days of detailed queries).


1. Log in to the **Admin Console**.

2. In the left navigation bar, select **Zero Trust Access** \> **Gateway Config** \> **Application Gateway Access Statistics**.

3. View the following data dimensions:

   * **Data Overview**: Select a time range (up to 180 days) to view core metrics:

      * **Number of visiting employees**: Unique employees who accessed applications via the gateway.

      * **Number of App Visits**: Unique applications accessed.

      * **Number of visits**: Total access requests generated.

      * **Login number**: Successful logins authenticated via the gateway.

   * **TOP 5 Rankings**

      * **TOP 5 Visited Applications**: Apps ranked by access count, including visitor numbers.

      * **TOP 5 Visited Employees**: Employees ranked by access frequency.

   * **Traffic Trend**: Visualizes traffic fluctuations via a line chart. Use the toggle in the top\-right corner to switch between **Access Count** and **Access User Count**.


<span id="9c4ab401"></span>
# Managing SSL certificates

To secure HTTPS traffic, you must upload SSL certificates to the SealSuite Admin Console. These certificates are required when associating applications with an Application Gateway.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Zero Trust Access** \> **Gateway Config** \> **Certificate**.

3. On the **Certificate** page, click **Add certificate** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48a995733017457ab42bddd252f36cd1~tplv-goo7wpa0wc-image.image) </span>

4. Enter a certificate name and upload your SSL certificate (`.crt`/`.pem`) and private key (`.key`) files.

5. Maintenance: You can edit or delete certificates from the list.

> **Caution**: Deleting a certificate will break internal access for any applications currently relying on it.
