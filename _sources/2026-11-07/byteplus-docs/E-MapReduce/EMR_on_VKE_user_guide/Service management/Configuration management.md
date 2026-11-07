---
title: "Configuration management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_configuration_management"
---

The configuration management module of EMR on VKE is designed to facilitate users in managing service configurations from the EMR page, including adding custom configurations, modifying configurations, viewing configuration modification history, and more. EMR will prompt users as to whether the affected components need to be restarted for the configuration to take effect, based on the scope of the configuration changes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration is the core of a service, so many EMR features are implemented based on configuration, such as adding RayCluster via YAML, Spark automatically associating with Celeborn, and more.</div>


<span id="179d5d09"></span>
## Scope of configuration

As shown in the figure above, configurations are categorized by scope. If the role column is empty, it represents an application\-level configuration, meaning that modifying this configuration is assumed to affect the entire application by default. If RayHistoryServer is configured, it represents a component\-level configuration, meaning that modifying this configuration will only affect that specific component.

When a configuration requires a restart to take effect, EMR will prompt the user with the list of components that must be restarted, as shown in the figure below:

<span id="a85cc595"></span>
## Configuration modification history

After modifying a configuration, the EMR page allows users to view the configuration history, as shown in the figure below:

<span id="05d191ce"></span>
## Configuration rollback

In the configuration management module of EMR on VKE, after a configuration is modified, if the new configuration causes issues or does not meet expectations, configuration rollback can be used to restore the configuration to a previous state. For example, after modifying configurations such as RayCluster, if the new configuration results in service exceptions, configuration rollback can be used to restore the configuration to its previous, normal state.

On the **configuration history** page, click the **rollback** button on the right side of the configuration file to roll back to a previous configuration state, as shown in the figure below:

<span id="7b1df13d"></span>
## what's next

The service must be restarted to apply the configuration after modification. For detailed instructions, see: Restart the service.
