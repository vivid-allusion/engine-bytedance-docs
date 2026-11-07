---
title: "Kibana common operations guide"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide_2"
---

The Kibana version provided by Cloud Search is compatible with the native Elasticsearch Kibana, but there are some operational differences between the two. This topic describes frequent operations for the Cloud Search version of Kibana.

<span id="1y2TxAdw"></span>
## Prerequisites

You have logged on to Kibana. For detailed steps, see [Log on to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

<span id="XAU0hm9m"></span>
## Statement execution

<span id="vNRkVGe7"></span>
### Execute DSL statements

Dev Tools is a commonly used toolkit in Kibana. You can execute DSL statements in Dev Tools to achieve various functions.


1. In the left navigation bar, select **Management \> Dev Tools**.

2. Enter the DSL statement to execute in the text box of the **Console** panel.

3. Click the execute icon at the top right corner of the text box.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc911ef54444c7c8bd8ec8701b6eb891.png) </span>


Additionally, you can click the configuration icon and select Auto intent to format the DSL statement as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ec721e5ce892cd3ae8a66138a35c9a7.png) </span>

<span id="rGJ9kLo4"></span>
### Execute SQL statements

You can execute SQL statements using the Query Workbench tool.


1. Select **Open Distro for Elasticsearch \> Query Workbench** in the left navigation bar.

2. Enter the SQL statement to execute in the text box of the **Query editor** panel.

3. Click the **Run** button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c217a47226bb56dea9b7504c3105479.png) </span>


<span id="TIjk7Gag"></span>
## Index type

<span id="ELG3elYs"></span>
### Create index pattern


1. Select **Management \> Stack Management** in the left navigation bar.

2. Select **Index Patterns**, then click **Create index pattern**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_361140c8de55ba4ddedc1ffb4c2ecb4a.png) </span>

3. Enter the index pattern name in the **Index pattern name** textbox, then click **Next step**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The index pattern name supports the wildcard <strong><code>*</code></strong><strong> </strong> to match multiple indices. Special characters <code>\\/?\"<>|</code> and spaces are not supported.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81807b68682289da7a33c0aa9f84e00c.png) </span>

4. Select **Time field** from the dropdown, choose **I don't want to use the time filter**, then click **Create index pattern**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a36d18b265d9e23cfa7bb265fe6d86f7.png) </span>


<span id="27CtwPwi"></span>
### View index list


1. Select **Open Distro for Elasticsearch \> Index Management** in the left navigation bar.

2. Select **Indices**, then view the index list in the **Indices** area.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbbb0d3d7ddd8206c5b1e07e1fdc778e.png) </span>


<span id="fvDxgAsB"></span>
### View index settings

Run the following command in Dev Tools. For more information, see [Execute DSL statements](https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide?lang=en#FDDR9cin).

```JSON
GET {index_name}/_settings
```


<span id="ldiH8HXs"></span>
### View index mapping

Run the following command in Dev Tools. For more information, see [Execute DSL statements](https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide?lang=en#FDDR9cin).

```JSON
GET {index_name}/_mapping
```


<span id="rl3MS9Gw"></span>
### Turn on an index

Run the following command in Dev Tools. For more information, see [Execute DSL statements](https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide?lang=en#FDDR9cin).

```JSON
POST {index_name}/_open
```


<span id="Ac1ozR3Q"></span>
### Turn off an index

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After turning off the index, data will remain but read/write services will no longer be available. You can reopen the index when needed.</div>


Execute the following command in Dev Tools. For more information, see [Execute DSL statements](https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide?lang=en#FDDR9cin).

```HTTP
POST {index_name}/_close
```


<span id="S6OU7py6"></span>
### Delete an index

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted indices cannot be recovered. Proceed with caution.</div>


Execute the following command in Dev Tools. For more information, see [Execute DSL statements](https://docs.byteplus.com/en/docs/cloudsearch/Kibana_common_operations_guide?lang=en#FDDR9cin).

```HTTP
POST {index_name}/_close
```


<span id="Fp1xdiZ6"></span>
## Query parameter settings

<span id="NxQ2u0gC"></span>
### Set the `max_concurrent_shard_requests` parameter


1. Select **Management \> Stack Management** from the left navigation bar.

2. Select **Advanced Settings**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c37d2f698f1faf34561c960f6aae5ac.png) </span>

3. On the **Settings** page, configure **Max Concurrent Shard Requests** to set the `max_concurrent_shard_requests` parameter.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9cd256f9d3732289114e7417e8ec1c9f.png) </span>


<span id="3Vf566w0"></span>
## Users and roles

This feature is available only to administrators, and operations differ slightly between Kibana 7.10.2 and Kibana 6.7.1.


<Tabs>
<Tab zoneid="ygFOm9CX" title="Kibana 7.10.2">
<TabTitle>Kibana 7.10.2</TabTitle>

<span id="SphGTWtD"></span>
### Create a role

You can define specific API permissions based on roles. For detailed permission information, refer to the [community official documentation](https://opendistro.github.io/for-elasticsearch-docs/docs/security/access-control/permissions/).

<span id="JAt7Giim"></span>
#### Procedure


1. Select **Open Distro for Elasticsearch \> Security** in the left navigation bar.

2. Select **Roles**, then click **Create role**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1a7947fc086984799a1210198ca81b9.png) </span>

3. On the **Create Role** page, configure the parameters as needed, then click **Create**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a696b61e55f40481e76fd6598b9d6096.png) </span>


<span id="fiC73SR0"></span>
### Create a user


1. Select **Open Distro for Elasticsearch \> Security** in the left navigation pane.

2. Select **Internal users**, then click **Create internal user**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca501b64395893299b58bbaadc0f4a5e.png) </span>

3. On the **Create internal user** page, configure the parameters as needed, then click **Create**.


<span id="wQlfrY1N"></span>
### Associate a role with user


1. Select **Open Distro for Elasticsearch \> Security** in the left navigation pane.

2. Select **Roles**, then click the target role name.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94051ec5f9c5934c2483b0cd1ec4e49b.png) </span>

3. On the target role details page, click the **Mapped users** tab, then click **Manage mapping**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf4af43738324c597409b8ea3f9c6cfd.png) </span>

4. On the **Map user** page, select the user to associate from the **Users** dropdown menu, then click **Map**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e6cf6161450d31359db00d739ba0c3b.png) </span>


</Tab>
<Tab zoneid="fOWbdh8q" title="Kibana 6.7.1">
<TabTitle>Kibana 6.7.1</TabTitle>

<span id="ImqNizLG"></span>
### Create a role

You can define specific API permissions based on roles. Refer to the [official community documentation](https://opendistro.github.io/for-elasticsearch-docs/docs/security/access-control/permissions/) for detailed permission names.

<span id="TurjkM3u"></span>
#### Procedure


1. Select **Security** in the left navigation bar, then click **Roles**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a1f5cd0e5f1ff43b3c55cb8283b27cb.png) </span>

2. On the **Roles** page, click  **+** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_197d1d87f90eda6b2a7a74e7157f45dc.png) </span>

3. On the **New Role** page, configure role parameters in each tab as needed, then click **Save Role Definition**. For detailed permission information, see the [Community official documentation](https://opendistro.github.io/for-elasticsearch-docs/docs/security/access-control/permissions/).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f028549e5db3fb0f5796db0c7a55ee7c.png) </span>


<span id="usrY9FwK"></span>
### Create a user


1. Select **Security** in the left navigation bar, then click **Internal User Database**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd19d38f9fc9a57b298034a6b24782df.png) </span>

2. On the **Manage Internal User** page, click  **+** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a14f1e2a214d56e4c1caa4265469b163.png) </span>

3. Configure each parameter as needed, then click **Submit**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ce213bae0eafa79ab23767669576213.png) </span>


<span id="CWNMexjC"></span>
### Associate roles to users


1. Select **Security** in the left navigation bar, then click **Role Mappings**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b83f2ac96c2b5b1357fbf8ebc59dbfd1.png) </span>

2. On the **Manage Role Mappings** page, click the target role name.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4eb4bcf1a17225e6666f4342f673c64.png) </span>

3. On the **Edit Role Mapping** page, click Add User, enter the user name to link, then click **Submit**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b55ce3e07a06978f28af965ca86d6b98.png) </span>


</Tab>
</Tabs>


<span id="miNAICDl"></span>
## Dev Tools index autocomplete

Dev Tools supports indices autocomplete as shown below. Operations differ slightly between Kibana 7.10.2 and Kibana 6.7.1.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15de8b3312322866fcfff11ec23c4dee.png) </span>


<Tabs>
<Tab zoneid="gC487Yvp" title="Kibana 7.10.2">
<TabTitle>Kibana 7.10.2</TabTitle>

1. Select **Open Distro for Elasticsearch \> Security** in the left navigation bar.

2. Select **Roles**, then click **Create role**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1a7947fc086984799a1210198ca81b9.png) </span>

3. On the **Create Role** page, enter the role name, add **indices:admin/template/get** permission under **Cluster permissions**, enter  **\***  under **Index**, add `indices:admin/get` and `indices:admin/aliases/get` permissions under **Index permissions**, then click **Create**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d4628cdfa0b73d3e15f01a0b49c6cca.png) </span>


</Tab>
<Tab zoneid="t64PqUMz" title="Kibana 6.7.1">
<TabTitle>Kibana 6.7.1</TabTitle>

1. Create an action group.

   1. Select **Security** in the left navigation, then click **Action Groups**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_478ca5eeadfffd5f221d9551327cec6a.png) </span>

   2. On the **Manage Action Groups** page, click  **+** .

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61856ca1071d8e600b62d9d0cdb50e7e.png) </span>

   3. On the **New Action Groups** page, enter the action group name, check **Show Advanced**, click **Add Single Permission**, select **indices:admin/template/get** from the dropdown, then click **Submit**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38329b57c71968e4a9050da73c671b43.png) </span>

2. Create a role.

   1. Select **Security** in the left navigation, then click **Roles**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_576ed021550a7ce4b58d06fc9087adfc.png) </span>

   2. On the **Roles** page, click  **+** .

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_197d1d87f90eda6b2a7a74e7157f45dc.png) </span>

   3. On the **New Role **  page, in the **Overview** tab, enter the role name.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb8c538b08cc1b4e697d5bd2d462197d.png) </span>

   4. Select the **Cluster Permissions** tab, click **Add Action Group**, then select the created action group from the dropdown.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_62c4c04ebef61a7604cdbb713637ae31.png) </span>

   5. Select the **Index Permissions** tab, then click **Add new index and document Type.** 

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_999b978c13ed9591d2d00986669c1ba6.png) </span>

   6. Enter  **\***  in the **Index** textbox, then click **Save**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96fda6b40a650f04b2f4c69a3997bf0b.png) </span>

   7. Check **Show Advanced**, click **Add Single Permission**, add the permissions `indices:admin/template/get`, `indices:admin/get`, and `admin/mappings/get` in order, then click **Save Role Definition**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb24cb0a8afe16ce346dc5659916df18.png) </span>

3. Associate the role with the user.

   1. Select **Security** in the left navigation bar, then click **Role Mappings**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b83f2ac96c2b5b1357fbf8ebc59dbfd1.png) </span>

   2. On the **Manage Role Mappings** page, click  **+** .

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffb53c38cd4ddfc924f2c5affe323d79.png) </span>

   3. Select the created role name from the **Role** dropdown, click **Add User**, enter the created user name, then click **Submit**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69032be8057c80fb7b0c0345bd211051.png) </span>


</Tab>
</Tabs>


<span id="KZw2MAvK"></span>
## Index lifecycle management

<span id="qCJfrBl2"></span>
### **Create a policy**


1. Select **Open Distro for Elasticsearch \> Index Management** in the left navigation bar.

2. Select **Index Policies**, then click **Create policy**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83d151d64a43f566f1683c2ac907b84a.png) </span>

3. On the **Create policy** page, set the **Policy ID**, define the policy content, then click **Create**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6259aa8b4e5ef32881a9219dacb2ea4.png) </span>


The created policy automatically applies to new indices. Below is an example policy to automatically delete indices after 7 days.

```JSON
{
    "policy": {
        "description": "Retain indices for 7 days",
        "default_state": "hot",
        "states": [
            {
                "name": "hot",
                "actions": [

                ],
                "transitions": [
                    {
                        "state_name": "delete",
                        "conditions": {
                            "min_index_age": "7d" // retention days
                        }
                    }
                ]
            },
            {
                "name": "delete",
                "actions": [
                   {"delete":{}}
                ],
                "transitions": [

                ]
            }
        ],
        "ism_template": {
            "index_patterns": [
                "index-*" // matching index patterns
            ]
        }
    }
}
```


<span id="AFRkUxPg"></span>
### **Associate a policy with an existing index**


1. Select **Open Distro for Elasticsearch \> Index Management** in the left navigation bar.

2. Select Indices, check the indices to associate, then click **Apply policy**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6498c2d77cfbe327d4c0d92212ff841.png) </span>

3. In the **Apply policy** dialog, select the policy to associate, then click **Apply**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20090274a5bc54c9401f5608537b72df.png) </span>


<span id="O36jyoX5"></span>
## More operations

Some features in the Kibana provided by Volcengine Cloud Search require Dev Tools to operate. If you need help, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) to contact the Volcengine Cloud Search service team.
