---
title: "CLB instance FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instance-faq"
---

## Feature description

### Does a CLB instance support backend FTP services?

Not supported yet.

### Does a CLB instance support editing HTTP headers?

Unsupported.

### Can a backend server act as a client to access the CLB instance?

If source IP address transparency is enabled, then no. Because the backend server will see the source IP of the packet as its own local IP and determine that the packet originated from itself, so it cannot return the response packet to the CLB instance, ultimately causing return traffic to fail.

If source address transparency is not enabled, then yes.

You can refer to [Configuring the backend server security groups](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group) to check whether the backend server's security group needs to allow client addresses (e.g., 0.0.0.0/0). If it does, then source address transparency is enabled, and the backend server cannot access the CLB instance as a client. If it does not, then source address transparency is not enabled, and the backend server can access the CLB instance as a client.

### Is the EIP assigned to a CLB instance dedicated?

Yes. The public IPs associated with public CLB instances and private CLB instances are not allowed to be bound to other cloud resources at the same time.

* After a public CLB instance is converted to a private CLB instance, the lifecycle of its associated EIP becomes independent from that of the CLB instance. After the EIP is unbound from the CLB instance, it can be rebound to other cloud resources.

* Similarly, after the EIP associated with a private CLB instance is unbound from the CLB instance, it can also be rebound to other cloud resources.

### Does CLB support the CONNECT method?

Unsupported.

### Does CLB support cross\-region?

Unsupported.

### Does CLB support configuring HTTP security headers?

Currently, BytePlus CLB listeners do not support directly configuring HTTP security headers. It is recommended that you implement them on backend servers (e.g., Nginx, Apache) by configuring response headers. For example, add the add_header directive in Nginx to configure security headers such as Content\-Security\-Policy and X\-Frame\-Options.

### Can CLB obtain the client source IP?

* Layer 4 CLB has source address transparency enabled by default, supporting direct retrieval of the client IP address.

   * When the backend server group is of IP type, or the client IP address is an IPv6 address while the backend server uses IPv4, the client IP address will be translated when the request passes through the CLB instance. In this case, you can [Obtain the client source IP using the Proxy Protocol](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address).

   * For a layer 4 CLB integrated with Web Application Firewall (WAF), the client IP address is translated when the request passes through WAF.

* Layer 7 CLB does not support obtaining the client IP address by default, but you can still obtain the client source IP by configuring the backend servers. For details, see [Obtaining the client source IP via Layer 7 listener](https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-7-listener-to-obtain-the-client-source-IP-address).

### Does CLB support TCP persistent connections?

Yes, supported. After establishing a TCP persistent connection, CLB supports continuous forwarding of business requests. Using TCP persistent connections reduces the number of TCP handshakes and helps improve the reuse rate of TCP connections.

### Can the VPC and subnet of a CLB instance be modified?

No. Plan the VPC and subnet information before creating a CLB instance. If you need to change the VPC or subnet after the instance is created, delete the instance and recreate it.

### Can the specifications of a CLB instance be adjusted?

Yes. You can [Modify specification](https://docs.byteplus.com/en/docs/clb/CLB-instances-03) on demand.

* For pay\-as\-you\-go instances, you can both upgrade and downgrade the specifications.

* For subscription (yearly/monthly) instances, only upgrades are supported; downgrades are not supported.

### Does a managed CLB instance support scaling?

Yes, supported. Managed CLB instances do not support scaling in the CLB console. However, scaling can be performed in the console of the service (e.g., container service) to which the managed CLB belongs. For detailed operations, see [Updating a CLB service](https://docs.byteplus.com/en/docs/vke/Managing-Services#.5pu05paw5pyN5Yqh).

### Does CLB support restricting client IP access?

Yes, supported. You can restrict client access traffic to CLB by setting ACL for the listener. For detailed operations, see [Setting ACL for a listener](https://docs.byteplus.com/en/docs/clb/Configuring-access-control-for-a-listener).

### How does CLB perform redirection?

Layer 7 listeners support redirection. You can redirect access requests matching a specific domain name and URL to another protocol, domain name, port, or path, and also specify a redirection status code. For detailed information, see [Adding a redirection forwarding rule](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule).

### Do CLB forwarding rules support rewriting?

CLB instances do not support rewriting. It is recommended to use the Standard Edition ALB.

## Actions

### Why can an IAM user who is granted the permission to deny applying for EIPs still create a public CLB?

Because the EIP address of a public CLB is a different product form from an EIP applied for separately. For example, the EIP of a public CLB cannot be bound or unbound. Therefore, granting an IAM user the permission to deny applying for EIPs does not affect their ability to create a public CLB.

When enabling the CLB service, you need to manually grant the CLB service cross\-service access permissions, and those permissions include APIs related to EIPs. Consequently, even if an IAM user is granted the permission to deny applying for EIPs, they can still obtain a new EIP by creating a public CLB.

If you need to deny IAM users the ability to create a public CLB, you can create a custom policy that denies creating a public CLB and attach it to the IAM user.

* For procedures, see [Creating a custom policy](https://docs.byteplus.com/en/docs/6257/1158323).

* Details of the policy that denies creating a public CLB are as follows:

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "clb:CreateLoadBalancer"
         ],
         "Condition": {
           "StringEqualsIfExists": {
             "clb:LoadBalancerType": [
               "public"
             ]
           }
         },
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```

### Under what circumstances does a CLB instance need an EIP?

When you need the CLB instance to accept requests from the public network, you must configure an EIP for it.

### Why is the Delete button grayed out on the CLB instance console, preventing deletion?

The prerequisites for deleting a CLB instance are as follows. If they are not met, deletion is not allowed.

* Ensure that the original business has been migrated or shut down.

* The CLB instance does not have modification protection enabled. If enabled, [Disable modification protection](https://docs.byteplus.com/en/docs/clb/CLB-instances-07) first.

* The CLB instance must be pay\-as\-you\-go or a subscription instance that has expired. .

* The CLB instance must not be bound to [PrivateLink](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01). If it is bound, see [Removing the service resources](https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources#.56e76Zmk5pyN5Yqh6LWE5rqQ).

* If, after checking the above, the CLB instance still cannot be deleted for an extended period, contact BytePlus[ Technical Support](https://console.byteplus.com/ticket/createTicketV2/).

### Can a CLB instance's IP be pinged?

When a client pings a CLB instance's IP, the request is responded to by the CLB cluster and is not forwarded to backend servers.

* Public CLB supports ping, and the instance is reachable by ping immediately after creation.

* Private CLB also supports ping, but only for clients within the same VPC or the same private network environment.

### Why does the CLB resource list only show the IDs of associated cloud resources (e.g., VPC, ECS, ENI) and not their names?

Because you are using an IAM user that does not have global permissions for the corresponding associated resources.

You need to grant the IAM user global permissions for those resources.

### Troubleshooting methods when backend services cannot be accessed through a CLB instance?

**Prerequisites**

Ensure that the backend server of this CLB instance is not being used as a client.

**Issue description**

When the following problems occur, refer to the following content to troubleshoot.

* Backend servers are directly accessible, but cannot be accessed through the CLB instance.

* The CLB instance is accessible via its private IP, but not via its EIP.

* Backend server health checks are exception.

**Background introduction**

1. Public clients access the CLB instance via its EIP; private clients access the CLB instance via its private IP.

2. The CLB instance forwards client traffic to the matching listener based on the listener protocol/port.

3. The listener first checks whether the backend server health checks are normal and forwards traffic only to normal backend servers.

4. The listener forwards traffic according to the scheduling algorithm and backend server weights.

From the above, the reasons why a client cannot access backend servers through the CLB instance may be related to security controls or health check configurations.

It is recommended that you troubleshoot in order from back end to front end to quickly identify the root cause.

#### Troubleshooting process

Step 1: Can you directly access the backend server: Use a client to directly access the backend server to confirm that the backend server configuration and business are working properly.

Step 2: Is the backend server configuration correct: Check whether the weight and service port of the backend server are correctly configured via the **backend server group**.

Step 3: Is the security group associated with the backend server correctly configured: Check via **Backend server \> Security group** whether the security group has allowed the service port and client access. For layer‑7 CLB, the 100.64 CIDR block must also be allowed. For detailed configuration, see [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

Step 4: If health checks are enabled on the listener, verify whether health checks are normal. Check via the **listener** whether the health check results are normal. When a health check is exception, the CLB instance does not forward traffic to that server. For detailed troubleshooting of exception health checks, see [Health check troubleshooting guide](https://docs.byteplus.com/en/docs/clb/Troubleshooting-health-check-exceptions).

Step 5: Is the access control configuration correct: Check via **CLB instance \> Basic information** whether access control is enabled and whether it is restricting client access.

If the problem persists after excluding the above issues, please contact your account manager.

### Why are backend server requests unbalanced?

|Possible causes |Troubleshooting process |
|---|---|
|Different backend servers have different weights |Check whether different weights have been configured for each backend server.<br><br>When the Weighted Round Robin algorithm is used, the CLB forwards access requests to backend servers in proportion to their configured weights. Different weights lead to different traffic distribution. In this case, an uneven distribution of request counts across different backend servers is considered normal. |
|The listener is configured with the Source IP Hash scheduling algorithm |Check whether the scheduling algorithm configured for the listener is Source IP Hash.<br><br>The Source IP Hash algorithm forwards access requests from the same IP address to the same backend server, which may result in an uneven distribution of request counts across different backend servers. This is normal. |
|ECS health check exception |Whether there have been health check failures or fluctuations during the relevant time period. See [Health check troubleshooting guide](https://docs.byteplus.com/en/docs/clb/Troubleshooting-health-check-exceptions) to find the cause. |
|The client has keep‑alive enabled |Check whether client requests have keep‑alive enabled<br><br>If keep‑alive is enabled on client requests, multiple HTTP requests from the same client in a short period may be forwarded to the same backend server, causing request imbalance. Adjust according to actual business needs. |

### How to unbind an EIP from a CLB instance?

* A public CLB instance does not support directly unbinding its EIP. However, you can first [convert it to a private CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-04), then unbind the associated EIP.

* For unbinding an EIP from a private CLB instance, see [Unbinding an EIP](https://docs.byteplus.com/en/docs/clb/CLB-instances-05).

### How to adjust the internet bandwidth of a CLB?

Public CLB instances and private CLB instances bound to an EIP support adjusting the internet bandwidth. For detailed steps, see [Modifying the internet bandwidth cap](https://docs.byteplus.com/en/docs/clb/CLB-instances-06).

### How to modify the file upload size limit of a CLB?

CLB itself does not support modifying the file upload size limit. It is recommended to check the `client_max_body_size` and `client_body_buffer_size` parameters in the backend Nginx configuration.

## Bandwidth related

### What is the difference between the bandwidth of a CLB instance and the bandwidth of its associated EIP?

* The CLB instance bandwidth refers to the bandwidth defined in the CLB instance specification, representing the maximum total traffic entering and leaving the CLB.

* The bandwidth of the EIP associated with the CLB instance refers to the maximum internet access traffic supported by that EIP.

Traffic from public clients accessing the CLB is limited by both the CLB instance bandwidth and the associated EIP bandwidth, and the smaller of the two values takes effect. Traffic from private clients accessing the CLB is limited only by the CLB instance bandwidth.

### Can the bandwidth of a CLB instance be adjusted?

* Different CLB instance specifications have different bandwidths. You can adjust the private network bandwidth of a CLB instance by [changing its specification](https://docs.byteplus.com/en/docs/clb/CLB-instances-03).

* Public CLB instances and private CLB instances bound to an EIP support adjusting the internet bandwidth limit. You can adjust the bandwidth by seeing [Modifying the internet bandwidth cap](https://docs.byteplus.com/en/docs/clb/CLB-instances-06).

### Does the bandwidth size of a CLB instance need to be adjusted based on the bandwidth of the backend servers?

The bandwidth of a CLB instance includes private bandwidth and internet bandwidth. Private bandwidth refers to the bandwidth defined in the CLB instance specification; Internet bandwidth refers to the bandwidth of the EIP associated with the CLB instance.

* It is the total private network traffic entering and leaving the CLB, and should be set according to the bandwidth required by private clients accessing the backend servers.

* Internet bandwidth used for traffic between public clients and the CLB instance. It should be adjusted based on actual backend business requirements.

## Quota related

### How many CLB instances or listeners can be created by default under a single account?

See [CLB usage limits](https://docs.byteplus.com/en/docs/clb/Product-Overview-07).

### Does the same CLB instance support binding multiple EIPs?

Unsupported.

* A public CLB instance is automatically associated with an EIP upon creation and does not require manual binding.

* A private CLB instance supports binding only one EIP per instance.

### What is a CLB quota?

To prevent resource abuse, BytePlus imposes limits on the number or capacity of service resources used. The maximum value of such a limit is called a quota. CLB quotas refer to resource quotas related to the CLB service. For details, see [Constraints and limits](https://docs.byteplus.com/en/docs/clb/Product-Overview-07).
