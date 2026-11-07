---
title: "Create a Data Source"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Create_a_Data_Source"
---

In a SaaS\-cloud native environment, you can create a Kafka, BMQ, or Webhook type data source based on the target data source requirements for data output. After the data source is created, the corresponding data source can be directly selected when subsequent data output tasks are created. This article describes the detailed steps and considerations for creating a data source.

<span id="191a97b5"></span>
# Background information

The types of data sources that SaaS\-cloud native environments support include:


* BytePlus Kafka

* BytePlus BMQ

* Webhook (whitelist limited opening)


<span id="ec9a6cf9"></span>
# Prerequisite


* The private network of North China 2 (Beijing) region has been created, and the subnet and security group corresponding to the VPC have been created. For activity details, please refer to [Create a Subnet ](https://docs.volcengine.com/docs/6401/67823?lang=en)and [Creating a security group](https://www.volcengine.com/docs/6401/68894).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec0c24be9ee49ca83a90535b90bb61f~tplv-goo7wpa0wc-image.image) </span>

* According to the event tracking data synchronization requirements, the target data source for the North China 2 (Beijing) region has been created: BytePlus Kafka or BMQ.

   * Gets the VPC network and subnet information that was bound when the data source was created.

      
      <Tabs>
      <Tab zoneid="PP9LIERPw4" title="Kafka">
      <TabTitle>Kafka</TabTitle>
      
      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc9bc371518438a9c025a1c24b49439~tplv-goo7wpa0wc-image.image) </span>
      
      
      </Tab>
      <Tab zoneid="mTuUFS6CG7" title="BMQ">
      <TabTitle>BMQ</TabTitle>
      
      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5c9480e18014bb5b85ddd09cd7f836e~tplv-goo7wpa0wc-image.image) </span>
      
      
      </Tab>
      </Tabs>
      

   * When using kafka, you also need to create a user of the kafka instance according to the data synchronization needs, and obtain the authentication information of the user. For activity details, please refer to the [Kafka user management help document ](https://www.volcengine.com/docs/6439/72043).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/570f35480c3548e59f10b4ee5b433838~tplv-goo7wpa0wc-image.image) </span>

* If you want to use webhooks for data output, you need to apply for whitelist activation in advance. If your webhook is deployed in BytePlus, you can obtain the VPC, subnet, and other information of the deployment environment in advance.


<span id="025d91f2"></span>
# Create a data source: Kafka

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you enable Kafka whitelist access, you need to add the data output network segment address to your Kafka whitelist. The IP network segment address to be added is: <code>66.192.0.0/16</code>.</div>



1. After logging in and entering the DataFinder product console, click on the top navigation bar **Data Management** \> **Data Output** \> **Custom Data Sources** to enter the **Custom Data Sources** page.

2. Click New Data Source in the upper right corner of the page to configure data source parameters in the side window that pops up.

3. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7851d50b718c440283f09d073ac037e8~tplv-goo7wpa0wc-image.image) </span>

   * Select the data source type as Kafka.

   * Select the access method in the drop\-down box. Currently, only BytePlus Kafka is supported.

   * Configure the data source name and description according to the interface prompts.

4. Parameter configuration. Select the created Kafka instance ID in the drop\-down box, and subsequent data will be transferred to the selected Kafka.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ddbdfeff7cf43e1a065568db6cf54ed~tplv-goo7wpa0wc-image.image) </span>

5. Network configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0774201001c540be9b113ce29eff3753~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Private networks, subnets, and security groups |Select the Kafka\-bound private network VPC and subnet.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc9bc371518438a9c025a1c24b49439~tplv-goo7wpa0wc-image.image) </span> |
   |Test access link |After completing the selection, click the test access link to test whether the network in the output transmission link is connected. The data source creation can only be completed after the test is successful. |
   

6. Authentication configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aae3d94796b24ea49c73ebac1112e327~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Authentication method |Select the authentication method based on the access point accessed by the service used when accessing Kafka:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f68a1362f6f047529755ae72d9cd7659~tplv-goo7wpa0wc-image.image) </span><br><br><br>* When using the **default access point** , select **NONE** without configuring the authentication username and key, Kafka protocol type PLAIN.<br><br>* When using **SASL_PLAINTEXT access points** , select **SCRAM\-SHA\-256** or **PLAIN** . The Kafka protocol type is SASL_PALINTEXT.<br><br>   * **The password type for SCRAM\-SHA\-256** is SCRAM.<br><br>   * **The PLAIN** password type is PLAIN. |
   |Username & Authentication Key |When the authentication method is **SCRAM\-SHA\-256** or **PLAIN** , it is configured to create the username and password corresponding to the Kafka account.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fd2a12e79c04f26ae6d512b2aaa0b7a~tplv-goo7wpa0wc-image.image) </span> |
   

7. Click **OK** to complete the data source creation.


<span id="6d453c7a"></span>
# Create a data source: BMQ


1. After logging in and entering the DataFinder product console, click on the top navigation bar **Data Management** \> **Data Output** \> **Custom Data Sources** to enter the **Custom Data Sources** page.

2. Click New Data Source in the upper right corner of the page to configure data source parameters in the side window that pops up.

3. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f9f03730eab4452ab4907aef22df60b~tplv-goo7wpa0wc-image.image) </span>

   * Select the data source type as BMQ.

   * Select the access method in the drop\-down box. The access method currently only supports BytePlus BMQ.

   * Configure the data source name and description according to the interface prompts.

4. Parameter configuration. Select the created BMQ instance ID in the drop\-down box, and subsequent data will be transferred to the selected BMQ.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f82ea000d5fa4c9b972714136191a867~tplv-goo7wpa0wc-image.image) </span>

5. Network configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afd15afd0a264d21a6533517fdddeaa9~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Private networks, subnets, and security groups |Select the BMQ\-bound private network VPC, subnet, and security group.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cccf8231e7b4652b467dd189f167613~tplv-goo7wpa0wc-image.image) </span> |
   |Test access link |After completing the selection, click the test access link to test whether the network in the output transmission link is connected. The data source creation can only be completed after the test is successful. |
   

6. Click **OK** to complete the data source creation.


<span id="f0ebb16d"></span>
# Create a data source: Webhook

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Webhook data source is not displayed by default, and can only be used after applying for whitelist opening.</div>


<span id="fd9a97a2"></span>
## Client side configuration

You need to add the exit Internet Protocol Address of the webhook to the whitelist of your data receiving server. The Internet Protocol Address to be added is: `180.184.72.215`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The exit Internet Protocol Address of the webhook will not change in most scenarios, but in very few scenarios it may change for some reason. If there is a change, DataFinder will notify you of the change. You can also contact BytePlus technical support to confirm whether the whitelisted address has changed before configuration.</div>


<span id="a9c35ce0"></span>
## DataFinder side configuration


1. After logging in and entering the DataFinder product console, click on the top navigation bar **Data Management** \> **Data Output** \> **Custom Data Sources** to enter the **Custom Data Sources** page.

2. Click New Data Source in the upper right corner of the page to configure data source parameters in the side window that pops up.

3. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55f4f91f8c9d4defbc407a095046db30~tplv-goo7wpa0wc-image.image) </span>

   * Select the data source type as Webhook.

   * Select the access method in the drop\-down box. Currently, HTTP and HTTPS are supported. You can choose according to the actual situation.

   * Configure the data source name and description according to the interface prompts.

4. Parameter configuration. Fill in the text box with the Webhook URL for the data to be transmitted.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4826077ae74d4e71bf0340b35fe86ca5~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Network configuration. If your webhook is deployed on BytePlus, you can configure the network configuration here and choose the VPC, subnet, and other environments where the webhook is deployed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bff7d1d1f57b45a298fd65cdcf4dd88e~tplv-goo7wpa0wc-image.image) </span>

   After completing the configuration, you can click the "Test Access Link" to test the configured webhook URL.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking "Test Access Link", DataFinder will send an empty POST command to the configured webhook, and the test of the access link can be passed when the status code returned by Response is "200". If the test results are unsuccessful, you can focus on the following:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Whether the network of the data receiving server is connected.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Whether the data receiving server level allows empty POST requests.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data receiving server level Whether to add Webhook exit IP to whitelist configuration.   </div>
   

6. Click **OK** to complete the data source creation.


<span id="e33efad1"></span>
# The next step is to create a data output task

Once you have created the data source, you can start creating the data output task, see details [Create Data Output Task](https://docs.byteplus.com/docs/DataFinder/Create_Data_Output_Task).
