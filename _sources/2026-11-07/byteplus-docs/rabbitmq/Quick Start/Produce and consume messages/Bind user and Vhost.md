---
title: "Bind user and Vhost"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost"
---

It is recommended to create a new non\-Admin user on the RabbitMQ cluster management Web UI before generating and consuming messages (directly using the administrator user is not recommended due to information leakage risks). Then bind the new user to a Virtual Host.

If a user is not bound to a Virtual Host, error messages like `access to vhost '/' refused for user 'xxx'` or `connection unauthorized` will show during production or consumption.

<span id="7a865a3e"></span>
## Operation steps


1. Log in to the RabbitMQ version instance Web UI.

   For operation steps, see [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. In the top menu bar, click the **Admin** tab.

3. Unfold **Add a user**, create a new non\-Admin user, then click **Add user**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b2a1dfde11643d69627f696f2d73109~tplv-goo7wpa0wc-image.image) </span>

4. In the **Users** area, find the newly created user and click the user name.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The new user is not yet bound to any Virtual Host and shows <code>No access</code>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62b8747c698d4803921ac18e2613b9be~tplv-goo7wpa0wc-image.image) </span>

5. In the **Permissions** section, bind a Virtual Host to the user, then click **Set Permission**.

   Every RabbitMQ server has a default vhost, namely "/". If you need to create a custom Virtual Host, see [Set up mirrored queue for instance](https://docs.byteplus.com/en/docs/rabbitmq/Set_up_mirrored_queue_for_instance).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f56fc450c6704d2ea6c40806e98545bc~tplv-goo7wpa0wc-image.image) </span>

6. Return to the **Admin** tab and check the Virtual Host bound to the user in the **Users** section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab14ecfdedff4628ae75f48547bc7f62~tplv-goo7wpa0wc-image.image) </span>
