---
title: "Associating a local workspace with a local Prometheus instance"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Associating_a_local_workspace_with_a_local_Prometheus_instance"
---

Vital Managed Service for Prometheus (VMP) provides local workspaces to associate the self\-built Prometheus instances of users, including Prometheus instances deployed in the virtual private clouds (VPCs). After association, you can use the VMP console to query the metrics of the corresponding workspaces in a centralized manner. This topic describes how to associate a local workspace with a self\-built Prometheus instance and use an aggregation query workspace for metric queries.

<span id="4sGD7GeN"></span>
## Prerequisites

A local Prometheus instance is deployed in a VPC, such as on an Elastic Compute Service (ECS) instance. The query URL and basic authentication are configured. For more details, refer to the [official documentation of Github](https://prometheus.io/docs/prometheus/latest/installation/).

<span id="uk5tabmx"></span>
## Procedure

<span id="rWEmBGew"></span>
### Step 1: Create a local workspace


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Workspace** in the left navigation pane to go to the workspace list page.

4. Click **Create**, and select the **Local workspace** tab to configure the local workspace.

   * **Basic information**: Specify the name of the local workspace and enter the query URL of the local Prometheus instance.

   * **Permission configuration**: Configure the authentication method of the local workspace. For this example, select Basic auth and enter the username and password of the local Prometheus instance.

   * **Network configuration**: In this example, the local Prometheus instance is deployed in a VPC of BytePlus. Therefore, select **Private network** and select the VPC and subnet where the local Prometheus instance is located.

5. Click **Confirm** to complete the configuration.


<span id="Z9gwqYq9"></span>
### Step 2: Configure a security group

After you create a local workspace and bind it to a local Prometheus instance deployed in a VPC, you need to configure a security group for the ECS instance on which the Prometheus instance is deployed. This ensures that the local workspace can access the local Prometheus instance as expected.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/securityGroup).  

2. In the top navigation bar, select the project and region to which the target resource belongs.

3. In the left navigation pane, click Security Group.

4. Find the security group where the ECS instance belongs in the security group list, and click the name of the security group to go to the security group details page.

5. Click the **Access rules** tab and click the **Inbound rules** tab. On the Inbound rules tab, click **Add rule** to add an inbound rule to the security group of the ECS instance. Here:

   * **Strategy**: Select **Allow**.

   * **Protocol type**: Select **TCP**.

   * **Port range**: Enter the port of the self\-built Prometheus instance, which is **9090** in most cases. Modify the value based on the actual situation.

   * **Source**: Select **CIDR**, and enter the CIDR where the elastic network interface (ENI) of the local workspace is located or enter `0.0.0.0/0`. In this example, `0.0.0.0/0` is entered.

6. Click **Add** to complete the configuration.


<span id="RHA7DLT1"></span>
### Step 3: Create an aggregation query workspace


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Workspace** to go to the workspace list page.

4. Click **Create**, and select the **Aggregated workspace** tab to configure the aggregation query workspace.

   * Specify a name for the aggregation query workspace.

   * Enable BasicAuth and configure the username and password.

   * Select a workspace to aggregate in the workspace list.

5. Click **Add** to complete the configuration.


<span id="ktvSrMp1"></span>
## Validate results

<span id="sfRJ1qGh"></span>
### Workspace query

After configuration, you can quickly query and display metric data by using the Explore feature.


1. Click **Explore** in the left navigation bar to go to the Explore page.

2. In the upper right corner of the page, select the configured aggregation query workspace, query time range, and data refresh method required for metric queries. Enter the metric that you want to query in the search box and click **Query**. The `__ws__` label will be added to the metrics, which indicates the ID of the workspace where the metrics belong, such as `__ws__: f7a69888-***`.
