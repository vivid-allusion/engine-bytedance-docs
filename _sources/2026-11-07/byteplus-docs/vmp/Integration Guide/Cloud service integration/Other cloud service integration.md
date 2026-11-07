---
title: "Other cloud service integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Other_cloud_service_integration"
---

<span id="r6oMUe5F"></span>
## Cloud services integrated with VMP

The following cloud services are integrated with VMP. You can refer to the corresponding documentation to complete the configuration.


|Cloud Service Name |References |
|---|---|
|Vital Container Instance (VCI) |[VCI integration](https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-Vital-Managed-Service-for-Prometheus) |
|API Gateway (APIG) |[APIG integration](https://docs.byteplus.com/en/docs/apig/Monitoring_and_Alerts) |


<span id="pmRDs3wa"></span>
## Cloud services not integrated with VMP

You can integrate other cloud services with VMP by using one of the following methods:


* Cloud Monitor integration: First integrate cloud services with Cloud Monitor and then integrate Cloud Monitor with VMP. For more details, refer to [Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services).

* Self\-managed integration: If cloud services support or provide a monitoring exporter, you can integrate the cloud services with VMP by deploying the exporter on an Elastic Compute Service (ECS) instance.
