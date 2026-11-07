---
title: "Purchase an ECS instance with the same configuration"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can use the "Purchase the same configuration instances" feature to quickly create a new instance based on an existing instance (the source instance), improving scale\-out efficiency in specific scenarios.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* The new instances to be created with this feature are in the same region and availability zone as the source instance. If you need to create an instance in a different region or availability zone, refer to [Purchasing an instance based on the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* If you associate more than 20 tags with the source instance, only the first 20 tags are retained for the instance to be created. To associate more tags with the new instance, manually associate tags after the instance is created. For more information, refer to[ Associating tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview#.5Yib5bu65bm257uR5a6a5qCH562-).

* If the source instance is a subscription\-based instance associated with a pay\-as\-you\-go volume, the instance to be created automatically associates the pay\-as\-you\-go volume.

* If you have adjusted the disk configuration of an instance created by using a whole image and want to purchase instances with the same configurations, the current instance configuration will be used for creating new instances. To purchase an instance with the same configuration as the whole image, you can [use the whole image to purchase an instance](https://docs.byteplus.com/en/docs/ecs/Using-whole-images-to-buy-ECS).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the project and region of the source instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. On the Instances page, select "··· \> Purchase the same configuration instances" in the "Actions" column of the target source instance.

   The system automatically fills in configurations of the source instance, and then redirects you to the "Confirm" page.

   > You can also modify the automatically filled configuration by clicking the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span> icon of the corresponding navigation page. Pay special attention to the parameters listed in the following table. For more parameter details, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).   
   

   
   |Navigation page |Parameter​ |Description |
   |---|---|---|
   |Network configuration |Secondary network interface |The secondary network interface of the instance to be created is the same as the first secondary network interface of the source instance. You can also click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span>icon next to "Network and security" to return to the network configuration page and modify the configurations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the source instance is associated with multiple secondary network interfaces, the instance created based on the source instance retains only one secondary network interface by default. To associate more network interfaces with the instance, you can manually <a href="https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces#.5oyC6L296L6F5Yqp572R5Y2h">mount network interfaces</a> after creating the instance.</div><br> |
   ||Security group |The security group associated with the secondary network interface of the new instance is exactly the same as that of the primary network interface. If you need to manage the security group associated with network interfaces, manually [change the security group](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups) after you create the instance. |
   |Custom configuration |Login credentials |* Password: If the source instance uses password\-based login, you need to specify a login password for the new instance.<br><br>* Key pair: If the source instance uses key pair\-based login, the new instance is automatically associated with the same key pair. |
   ||Instance name |By default, the system automatically generates instance names based on the product name. |
   ||Host name |By default, the system generates a hostname based on the ECS instance ID.<br><br>You can also modify the hostname as needed after creating the instance. For more information, refer to [Changing instance hostname](https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance). |
   ||Deployment set |The instance to be created is not automatically associated with the deployment set. After creating an instance, you can add the instance to a deployment set as needed. For more information, refer to [Changing the deployment set of an instance](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview). |
   |Order confirmation |Instance quantity |The number of instances to be created. The default value is 1. You can modify the number as needed at the bottom of the page. |
   ||Subscription duration |The subscription duration. The default subscription duration is one month. You can adjust the duration as needed on the "Confirm" page. |
   ||Enable automatic renewal |For subscription instances, specify whether to enable the "Enable automatic renewal" option. This option is disabled by default.<br><br>> Once automatic renewal is enabled, the system automatically deducts the renewal fee from your account balance before the instance expires. You do not need to manually renew the instance. |
   

5. Follow the console guidance to review and confirm the relevant agreements (if any).

6. Click "Buy now". On the order confirmation page, review the order information and complete the payment.

   > If you have available coupons, ​select them for fee deduction.   
   

7. After you make the payment, click the "Go to Console" button to be redirected to the Instances page, where you can view the new instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After purchasing an instance, you can follow the [Subsequent operation](https://docs.byteplus.com/en/docs/ecs/What-to-do-next) to learn and use ECS instances.

<span id="aVyFTZKX"></span>
## FAQ


* [How do I configure a domain name? What conditions must be met for domain name filing?](https://docs.byteplus.com/en/docs/ecs/What-to-do-next#.6YWN572u5Z-f5ZCN)

* [How can I view the regions and availability zones where instances are available for sale?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5p-Q5Liq5Zyw5Z-f5oiW5Y-v55So5Yy65piv5ZCm6IO96LSt5Lmw5a6e5L6L77yf)

* [What should I do when "Sold out" appears when I purchase an instance of a particular specification?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6LSt5Lmw5p-Q6KeE5qC855qE5a6e5L6L5pe277yM5pi-56S64oCc5bey5ZSu572E4oCd5oCO5LmI5Yqe77yf)

* [Can I buy ECS instances if my account does not undergo real-name authentication?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5rKh5pyJ6YCa6L-H5a6e5ZCN6K6k6K-B6IO95LiN6IO96LSt5Lmw5LqR5pyN5Yqh5Zmo5a6e5L6L77yf)

* [How long does it take to use an ECS instance after I purchase one?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6LSt5Lmw5LqR5pyN5Yqh5Zmo5ZCO5aSa5LmF6IO95L2_55So77yf)


For more questions about purchasing instances, refer to [FAQs on purchasing instances](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6LSt5Lmw5a6e5L6L6Zeu6aKY).
