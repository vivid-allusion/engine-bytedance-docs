---
title: "Spring Boot SDK"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Spring_Boot_SDK"
---

This topic describes how to use Spring Boot to connect to a RabbitMQ instance for message production and consumption under the AMQP protocol, and provides corresponding sample code.

<span id="d9b824eb"></span>
## Preparations


* Obtain the AMQP access point from the RabbitMQ instance details page. To enable public network access for an instance, see [Set up public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access).

* Directly using administrator users for production and consumption may pose a risk of information leakage. Before performing production and consumption, you need to create a new user with a non\-Admin role in the RabbitMQ Cluster management Web UI and bind a Virtual Host to this user. For the steps, please refer to [Bind users and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost).

* Create a queue and an exchange in advance on the RabbitMQ Cluster management Web UI.


<span id="e0da8dc0"></span>
## Add dependencies

Add the following dependencies to the `pom.xml` file:

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
    <version>2.3.1.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.3.1.RELEASE</version>
</dependency>
```


<span id="008c4a24"></span>
## Prepare the configuration file

Create the configuration file `application.yml` in the `resources` directory. After correctly filling in the RabbitMQ instance\-related configuration, enter the following content into the configuration file.

```XML
spring:
  rabbitmq:
    host: rbtmq-516***.rabbitmq.xxx.com
    port: 5671
    virtual-host: /
    username: doc-user
    password: user-password
    # If the instance has public network access enabled, the following information needs to be configured.
    ssl:
      enabled: true
      algorithm: TLSv1.2
      verify-hostname: false
      validate-server-certificate: false
```


<span id="f7ffdcfc"></span>
## Produce message

```Java
package org.example;

import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ProducerController {

    @Autowired
    private RabbitTemplate rabbitTemplate;

    @RequestMapping("/send")
    public String sendMq(String msg) {
        rabbitTemplate.convertAndSend("doc-exchange", "doc-routekey", msg);
        return "send ok";
    }

}
```


<span id="fea8f26e"></span>
## Consume messages

```Java
package org.example;

import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.stereotype.Component;

@Component
public class ConsumeService {

    @RabbitListener(queues = "doc-queue")
    public void receive(String message) {
        System.out.println("consume msg:" + message);
    }
}
```


<span id="9aac0745"></span>
## Verify results

After starting the Spring Boot application, you can access `http://localhost:8080/send?msg=xxx` in your browser and then send the target message. After a successful send, `send ok` will be returned.
