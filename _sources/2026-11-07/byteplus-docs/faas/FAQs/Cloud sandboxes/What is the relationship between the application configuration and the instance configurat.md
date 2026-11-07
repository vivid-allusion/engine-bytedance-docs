---
title: "What is the relationship between the application configuration and the instance configuration in the cloud sandbox?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Relationship_between_the_application_configuration_and_the_instance_configuration"
---

The configuration at the sandbox instance level overrides the configuration at the application level. If an instance is not configured separately, it will, by default, inherit and reuse the configuration of its associated sandbox application. The specific relationship is as follows:


* **Storage mount**: An instance can mount the same storage as the application, but can select a different mount directory. If the instance is not configured, it fully reuses the application's mount configuration.

* **Image**: An instance can be configured with a different image version from the application. If the instance is not configured, it reuses the application's image.

* **Environment variable**: An instance can set new environment variables or override environment variables inherited from the application. If the instance is not configured, it fully reuses the application's environment variables.
