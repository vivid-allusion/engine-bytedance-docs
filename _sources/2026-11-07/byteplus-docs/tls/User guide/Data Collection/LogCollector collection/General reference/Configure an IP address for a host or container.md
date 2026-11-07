---
title: "Configure an IP address for a host or container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/configure_an_ip_address_for_a_host_or_container"
---

Torch Log service (TLS) allows you to specify a custom IP address for a LogCollector host and change the policy based on which LogCollector get the IP address of the current host. This helps identify and manage hosts in host groups. This topic describes how to set a custom IP address for a host or container.

<span id="背景信息"></span>
## Background

TLS LogCollector gets the IP address of the host or container on which it resides. This can help you identify and manage hosts and containers in host groups. By default, LogCollector uses the IP address of the first network interface of a host or container as the IP address of the host or container and reports it to the TLS server. You can also specify a custom IP address for a host or container, or change the policy based on which LogCollector gets the IP address of the current host or container based on your business requirements.

If both a policy of getting the IP address of the current host or container and an IP address are set, the specified IP address is used.


|Setting Method |Description |
|---|---|
|Setting a policy of getting IP addresses |To set a policy for LogCollector to get the IP address of the current host, configure the ip_policy parameter in the LogCollector configuration file. By default, LogCollector uses the IP address of the first network interface of a host or container as the IP address of the host or container. You can change the policy for LogCollector to get the IP address of a specified network interface or get the IP address of the current host or container based on the specified order. For more information, refer to [Policy overview](https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container#%E7%AD%96%E7%95%A5%E8%AF%B4%E6%98%8E).<br><br>This method is suitable for scenarios where you collect logs from containers or hosts in label\-based host groups. |
|Specifying an IP address |To specify a fixed IP address for a host, set the `ip` parameter in the LogCollector initiation configuration when installing LogCollector on the host. After LogCollector is installed, you can modify the configuration file to change the IP address. For more information, refer to [Specify an IP address](https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container#%E6%8C%87%E5%AE%9A-ip-%E5%9C%B0%E5%9D%80).<br><br>This method is suitable for scenarios where you collect logs from hosts in IP address\-based host groups. |


<span id="设置-ip-地址获取策略"></span>
## Set a policy of getting IP addresses

TLS identifies hosts and containers in a host group by IP addresses. In label\-based host groups, the IP addresses of hosts or containers obtained by LogCollector may change, causing you fail to distinguish or identify hosts or containers. In this scenario, you can set the policy for LogCollector to get the IP address of the current host or container. For example, set it to get the IP address of the specified network interface or get the IP address of the current host or container based on the specified order.

<span id="策略说明"></span>
### Policy overview

TLS identifies hosts and containers in host groups by IP addresses. LogCollector automatically gets and reports the IP address of its host to the TLS server. By default, LogCollector uses the IP address of the first network interface as the IP address of the current host or container. You can change the policy for LogCollector to get the IP address of the current host or container as needed.

TLS LogCollector supports the following policies of getting IP addresses:


* Using the IP address of the first network interface as the IP address of the current host or container. This is the default policy.

* Using the IP address of the specified network interface as the IP address of the current host or container. If LogCollector successfully get the IP address of the specified network interface, it uses the IP address gotten as the IP address of the current host or container. Otherwise, it uses the IP address of the first network interface instead.

* Getting the IP address in the order of hostname \> eth0 \> bond0. If LogCollector successfully get the IP address, it uses the IP address gotten as the IP address of the current host or container. Otherwise, it performs the next step to get the IP address. If it fails to get an IP address after performing all steps, it uses the IP address of the first network interface.


<span id="设置方式"></span>
### Set Method

Add the `ip_policy` parameter to `output.tls` in the configuration file. This parameter is used to specify the strategy for LogCollector to obtain IP addresses. The paths of the configuration files are as follows:


* For versions prior to Logcollector v2.2.0: `/usr/local/filebeat - 7.12.0/etc/filebeat.yml`

* For Logcollector v2.2.0 and subsequent versions: `/usr/local/logcollector/etc/logcollector.yml`


For instructions on how to check the LogCollector version, please refer to [2 View software version](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After changing the settings, restart LogCollector to apply the changes. For more information on how to restart LogCollector, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E8%BF%9B%E7%A8%8B%E7%AE%A1%E7%90%86">Managing processes</a>.</div>


You can configure the `ip_policy` parameter as follows:


|Parameters |Description |
|---|---|
|`ip_policy：''` |LogCollector uses the IP address of the first network interface as the IP address of the current host or container. This is the default setting. |
|`ip_policy：'hostname'` |Getting the IP address in the order of hostname \> eth0 \> bond0. |
|`ip_policy：'NETWORK_INTERFACE_NAME'` |Using the IP address of the specified network interface as the IP address of the current host or container. |


For example, to use the IP address of eth1 as the IP address of the current host, the configurations are as follows:

```yaml
output.tls:
  endpoint: 'https://tls-ap-southeast-1.bytepluses.com'  #--The TLS endpoint
  secret_id: Your AccessKey ID                      #--The AccessKey ID of your account
  secret_key: Your AccessKey Secret                    #--The AccessKey Secret of your account
  region: ap-southeast-1                              #--The Region where the project resides
  compress_type: lz4                              #--The compression type. We recommend that you use the default value: lz4.
  label: http_module                              #--The custom host label
  ip_policy: 'eth1'                               #--The policy of getting the IP address of the current host
```


<span id="指定-ip-地址"></span>
## Specify an IP address

To collect logs from a host in an IP address\-based host group, you must add the IP address that LogCollector obtains from the host to the host group. Otherwise, the heartbeat status of LogCollector installed on the host may be exceptional due to IP address mismatch. If the IP address obtained by LogCollector is inappropriate for your business, or the supported policies of getting IP addresses do not meet your business requirements, specify an IP address for the current host as described below.


* **Specify an IP address when installing LogCollector**:

   Configure the `ip` parameter to specify an IP address for the current host during initiation. For more information, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host). When creating a host group, add the specified IP address to the host group. Then, the IP address is displayed as the identifier of the host in the host group.

* **Changing the IP address after installing LogCollector**:

   During the operation of LogCollector, if you need to modify authentication parameters such as `secret_id` and `secret_key`, or identification parameters of LogCollector such as `label`, you can execute the following commands to modify the LogCollector configuration file.

   ```YAML
   sudo /usr/local/logcollector/tools/logcollector.sh update_config --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --label {label} 
   ```
   

   For detailed descriptions of parameters such as `region`, `endpoint`, `secret_id`, and `secret_key`, please refer to [2 View software version](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#%E6%9F%A5%E7%9C%8B%E8%BD%AF%E4%BB%B6%E7%89%88%E6%9C%AC).
