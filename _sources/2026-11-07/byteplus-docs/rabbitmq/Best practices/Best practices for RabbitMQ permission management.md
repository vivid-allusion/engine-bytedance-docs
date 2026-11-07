---
title: "Best practices for RabbitMQ permission management"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_permission_management_best_practices"
---

<span id="SsINhz4o"></span>
## Overview

This topic describes the authentication and authorization features in RabbitMQ, which work together to help operators control system access. Different users can be granted permission to access only specific virtual hosts, and their permissions within each virtual host can also be restricted. RabbitMQ supports two main authentication mechanisms and multiple authentication and authorization backends.

<span id="GNAOWUOb"></span>
## Fundamentals

When a client connects to RabbitMQ, it provides a set of credentials: a username/password pair, a JWT token, or an x.509 certificate. Each connection is associated with an authenticated user. It also targets a virtual host, and the user must have specific permissions for that virtual host.

User credentials, target virtual host, and the optional client certificate are specified when the connection starts. There is a default set of credentials, called the default user. By default, this user can only connect locally to the host; remote connections using the default user are denied. Do not use the default user in production environments. Create new user accounts with generated credentials.

After the application connects to RabbitMQ, it must authenticate—that is, provide and confirm its identity—before performing operations. With this identity, the RabbitMQ node can look up permissions and authorize access to virtual hosts, queues, exchanges, and other resources.

The two main client authentication methods are username/password pairs and X.509 certificates.


* Username/password pairs can be used with various authentication backends for verifying credentials. Connections that fail authentication are closed, and an error message is recorded in the server log.

* To authenticate client connections with X.509 certificates, enable the built\-in `rabbitmq-auth-mechanism-ssl` plugin and configure the client to use the EXTERNAL mechanism. With this mechanism, any password provided by the client will be ignored.


<span id="Ng6p9Ntt"></span>
## Manage users and permissions

Add one administrator account for reading and writing, and another for operations management using the following methods. Use separate administrator accounts for data access and operations to avoid permission escalation and account mixing.


* Add an account through the open\-source RabbitMQ console. For details, see the open\-source RabbitMQ [product documentation](https://www.rabbitmq.com/docs/3.13).

* Add an account through the BytePlus RabbitMQ Edition console. For detailed instructions, refer to step 7 in [Create Instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance_1).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Do not modify administrator accounts and passwords that were added through the BytePlus RabbitMQ Edition console in the open\-source RabbitMQ console. If changes are needed, make them directly in the BytePlus RabbitMQ Edition console.</div>


<span id="YlzJe6r2"></span>
## Authorization: How permissions work

When a RabbitMQ client connects to the server and authenticates, it specifies a virtual host for running. At this point, the first level of access control is enforced. The server checks if the user has permission to access the virtual host and rejects the connection if not.

Resources, such as exchanges and queues, are named entities within a specific virtual host. The same name in different virtual hosts refers to distinct resources. The second level of access control is enforced when performing operations on resources.

RabbitMQ distinguishes `configure`, `write`, and `read` operations on resources


* `Configure` operations create or destroy resources, or change their behavior

* `Write` operations inject messages into resources

* `Read` operations retrieve messages from resources


To perform actions on resources, users must be granted the appropriate permissions


<Tabs>
<Tab zoneid="jBCVIaD4CF" title="AMQP 0-9-1">
<TabTitle>AMQP 0-9-1</TabTitle>

The table below shows which types of permissions are required for each AMQP 0\-9\-1 command that checks execution permissions for resources.


|**AMQP 0\-9\-1** | |**Configuration** |**Write** |**Read** |
|---|---|---|---|---|
|exchange.declare |(passive=false) |exchange |\- |\- |
|exchange.declare |(passive=true) |\- |\- |\- |
|exchange.declare |(with [AE](https://www.rabbitmq.com/docs/3.13/ae)) |exchange |exchange (AE) |exchange |
|exchange.delete |\- |exchange |\- |\- |
|queue.declare |(passive=false) |queue |\- |\- |
|queue.declare |(passive=true) |\- |\- |\- |
|queue.declare |(with [DLX](https://www.rabbitmq.com/docs/3.13/dlx)) |queue |exchange (DLX) |queue |
|queue.delete |\- |queue |\- |\- |
|exchange.bind |\- |\- |exchange (destination) |exchange (source) |
|exchange.unbind |\- |\- |exchange (destination) |exchange (source) |
|queue.bind |\- |\- |queue |exchange |
|queue.unbind |\- |\- |queue |exchange |
|basic.publish |\- |\- |exchange |\- |
|basic.get |\- |\- |\- |queue |
|basic.consume |\- |\- |\- |queue |
|queue.purge |\- |\- |\- |queue |





</Tab>
<Tab zoneid="Fs5xTS0uuP" title="MQTT">
<TabTitle>MQTT</TabTitle>

MQTT protocol does not include concepts of exchanges, queues, or bindings. Our MQTT extension is built on the AMQP protocol and uses the same permission system. You can learn more in the [MQTT Plugin](https://www.rabbitmq.com/docs/mqtt).

The table below shows which type of resource each MQTT command requires permissions for when performing permission checks.


|**MQTT actions** | |**Configuration** |**Write** |**Read** |
|---|---|---|---|---|
|SUBSCRIBE |\- |queue |queue |exchange |
|PUBLISH |\- |\- |amq.topic |\- |
|PUBLISH |non\-default exchange |\- |exchange |\- |


The PUBLISH action also requires topic authorization.


</Tab>
</Tabs>


Permissions are expressed as ternary regular expressions, with configuration, write, and read permissions corresponding to each virtual host Users are granted operation permissions for all resources whose names match the regular expressions For example, the table above shows that the `queue.bind` protocol operation requires write permission for the target queue and read permission for the target exchange

In other words, to allow a user to bind a queue named `queueA` to an exchange named `exchangeB`, the user will need a write permission regular expression (for the correct virtual host) that matches `queueA`, and a read permission regular expression that matches `exchangeB` For convenience, RabbitMQ maps the empty name of the default AMQP 0\-9\-1 exchange to "amq.default" during permission checks

The regular expression `'^$'` (which matches only an empty string) covers all resources and effectively prevents users from performing any actions Built\-in AMQP 0\-9\-1 resource names use `amq.` as a prefix, while server\-generated names use `amq.gen` as a prefix For example, `'^(amq\.gen.*|amq\.default)$'` allows users to access server\-generated names and the default exchange The empty string `''` is synonymous with `'^$'`, restricting permissions in exactly the same way

RabbitMQ may cache access control check results based on each connection or each channel Therefore, changes to user permissions may only take effect when users reconnect For details on setting up access control, see the [User and Permissions Management](https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_permission_management_best_practices?lang=zh#Ng6p9Ntt) section and the [rabbitmqctl documentation](https://www.rabbitmq.com/docs/man/rabbitmqctl.8).

<span id="m6zuFg6p"></span>
## More references

For more information on permission management for authentication, authorization, and access control, refer to the open\-source RabbitMQ [Authentication, Authorization, and Access Control](https://www.rabbitmq.com/docs/3.13/access-control#overview).

&nbsp;
