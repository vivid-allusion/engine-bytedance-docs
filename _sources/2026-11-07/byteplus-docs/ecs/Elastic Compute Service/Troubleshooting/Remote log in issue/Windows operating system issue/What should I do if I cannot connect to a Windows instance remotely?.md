---
title: "What should I do if I cannot connect to a Windows instance remotely?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log__into_a_Windows_instance"
---

When you use a local computer running the Windows operating system to connect to a Windows ECS instance via Remote Desktop Protocol (such as MSTSC), an error occurs. The following error messages are displayed:


* Prompt: Remote Desktop cannot connect to the remote computer. Make sure that the remote computer is turned on and connected to the network, and that remote access is enabled.

   Refer to the following content to check and [enable the RDP service on the ECS instance](https://docs.byteplus.com/en/docs/ecs/Method_for_enable_Remote_Desktop_Connection_RDP_service_for_Windows_system_instances).

* Prompt: An authentication error has occurred. The function requested is not supported. This could be due to a CredSSP encryption database correction.

   Such an error message may be caused by a security patch released by Microsoft in April 2018. When a local computer uses a newer version of the RDP client to access an unpatched Windows Server, the remote connection is blocked by CredSSP. For solutions, refer to the [documentation on the Microsoft official website](https://support.microsoft.com/zh-cn/topic/cve-2018-0886-%E7%9A%84-credssp-%E6%9B%B4%E6%96%B0-5cbf9e5f-dc6d-744f-9e97-7ba400d6d3ea).
