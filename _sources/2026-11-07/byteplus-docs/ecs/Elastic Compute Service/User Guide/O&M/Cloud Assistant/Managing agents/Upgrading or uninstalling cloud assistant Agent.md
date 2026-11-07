---
title: "Upgrading or uninstalling cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Upgrading-or-uninstalling-agents"
---

You can upgrade the cloud assistant Agent to gain access to new features, address known vulnerabilities, improve performance, or enhance the user experience. If you no longer need to use the cloud assistant Agent, for reasons such as business restrictions, port conflicts, or compliance requirements, you can also uninstall the cloud assistant Agent.

<span id=".5Y2H57qn5a6i5oi356uv"></span>
## Upgrade the cloud assistant Agent

If the cloud assistant Agent is not updated to the latest version and the Agent status is **In service**, you can upgrade it to the latest version in one click.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Note that when an Agent upgrade (either automatic upgrade or manual upgrade) is performed on a Linux system, the <code>daemon-reload</code> command will be executed. This may impact your business (for example, configuration will be reloaded), so please proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">By default, the system automatically upgrades at random times daily between 14:00 and 18:00. If you want to disable this automatic upgrade feature, follow the steps below:</div>


   1. <div data-tips="true" data-tips-type="tip">Log in to the target instance. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance">Logging in to Linux instances</a>.</div>


   2. <div data-tips="true" data-tips-type="tip">Edit the configuration file.</div>


      <div data-tips="true" data-tips-type="tip">      ```Plain Text
      /usr/local/assist-client/assist_client_conf.json        
      ```
            </div>
      

   3. <div data-tips="true" data-tips-type="tip">Set <code>AutoUpdate</code> to <code>false</code>.</div>


   4. <div data-tips="true" data-tips-type="tip">Execute the following command to restart the instance.</div>


      <div data-tips="true" data-tips-type="tip">      ```Plain Text
      systemctl restart assist-client.service
      ```
            </div>
      

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Agent management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select target instances to upgrade the cloud assistant Agent.

   * **Upgrade the cloud assistant Agent for multiple instances**

      1. From the instance list, select target instances that require the ​upgrade of the cloud assistant Agent.

         > You can select up to 50 instances at a time.         
         

      2. Below the list, click the "Upgrade" button.

      3. Confirm whether you can upgrade selected instances. If you can not upgrade some selected instances, click the "Disallow upgrade instance" tab to resolve issues as instructed, and then upgrade instances. Or ignore instances on the "Disallow upgrade instance" tab first and click the "Confirm" button to upgrade instances on the "Allow upgrade instance" tab.

   * **Upgrade the cloud assistant Agent for one instance**

      1. Search for or query information about the target instance from the instance list.

      2. Click the "Upgrade" button in the "Action" column on the right side of the target instance to complete the operation.

4. After the upgrade is complete, the Agent status changes to **In service**.


<span id=".5Y246L295a6i5oi356uv"></span>
## Uninstall the cloud assistant Agent

If you no longer need to use the cloud assistant Agent, for reasons such as business restrictions, port conflicts, or compliance requirements, you can also uninstall the cloud assistant Agent in the **In service** state.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Agent management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select target instances to uninstall the cloud assistant Agent.

   * **Uninstall the cloud assistant Agent for multiple instances at the same time**

      1. On the Agent management page, select multiple target instances that require uninstalling the cloud assistant Agent.

         > You can select up to 50 instances at a time.         
         

      2. Below the list, click the "Uninstall" button.

      3. Confirm whether you can uninstall selected instances. If you can not uninstall some selected instances, click the "Disallow uninstall instance" tab to resolve issues as instructed, and then uninstall instances. Or ignore instances on the "Disallow uninstall instance" tab first and click the "Confirm" button to uninstall instances on the "Allow uninstall instance" tab.

   * **Uninstall the cloud assistant Agent for one instance**

      1. Search for or query information about the target instance from the instance list.

      2. Click the "Uninstall" button in the "Action" column on the right side of the target instance to complete the operation.

4. After the uninstallation is complete, the Agent status changes to **Uninstalled**.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [UpgradeCloudAssistants-Upgrades the cloud assistant Agent version](https://docs.byteplus.com/en/docs/ecs/UpgradeCloudAssistants_-_Upgrade_Cloud_assistant_Agent)

* [UninstallCloudAssistants - Uninstalls the cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/UninstallCloudAssistants_-_Uninstall_Cloud_assistant_Agent)
