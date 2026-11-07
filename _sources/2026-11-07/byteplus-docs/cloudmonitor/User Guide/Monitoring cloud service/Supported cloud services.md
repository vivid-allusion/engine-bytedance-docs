---
title: "Supported cloud services"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics"
---

The following table lists cloud services that are integrated with Cloud Monitor. When you use these cloud services, the system will automatically enable monitoring for the services and report metrics.


|**Service Category** |**Service Name** |**Namespace** |Data Storage Duration (Days) |
|---|---|---|---|
|Elastic Computing |Elastic Compute Service (ECS) |VCM_ECS |60 |
||Dedicated Host (DDH) |VCM_DDH |60 |
||AgentKit\-MCP |VCM_AgentKitMcp |30 |
||AgentKit\-agent runtime |VCM_AgentKitRuntime |30 |
||AgentKit\-tool |VCM_AgentKitSandboxTool |30 |
|Container |Vital Kubernetes Engine (VKE) |VCM_VKE |30 |
|CDN and acceleration |Content Delivery Network (CDN) |VCM_CDN |30 |
||Full site acceleration |VCM_DCDN |30 |
||Global Accelerator (GA) |VCM_GA |30 |
||Edge Networking SD\-WAN |VCM_SDWAN |30 |
||Edge Computing \- Edge Intelligence |VCM_VEI |30 |
|Video Cloud |Video on Demand (VOD) |VCM_VOD |30 |
||VOD \- CDN |VCM_VODCDN |30 |
||velmageX |VCM_veImageX |30 |
||Video Live Streaming |VCM_LIVE |60 |
|Serverless |Function Service (veFaaS) |VCM_veFaaS |30 |
|Database |Database Transmission Service (DTS) |VCM_DTS |30 |
||Table Database HBase |VCM_HBase |30 |
||Table Database HBase Edition \- multiple availability zones |VCM_MultiazHBase |30 |
||Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |30 |
||Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |30 |
||RDS for MySQL Sharding edition |VCM_MySQL_Sharding |30 |
||RDS for MySQL |VCM_RDS_MySQL |30 |
||RDS for PostgreSQL |VCM_RDS_PostgreSQL |30 |
||RDS for SQL Server |VCM_RDS_SQLServer |30 |
||RDS for veDB MySQL |VCM_veDB_MySQL |30 |
||Cache for Redis \- Community Edition |VCM_Redis |30 |
||Cache for Redis \- Enterprise Edition |VCM_Redis_Enterprise |30 |
||Graph Database veGraph |VCM_veGraph_db |30 |
|Storage |CloudFS |VCM_CFS |30 |
||EBS |VCM_EBS |60 |
||SFCS |VCM_SFCS |30 |
||NAS extreme speed |VCM_FileNAS |30 |
||NAS capacity type |VCM_veFileNAS |30 |
||NAS cache type |VCM_veFileNAS_Cache |30 |
||NAS vePFS |VCM_vePFS |90 |
||Torch Object Storage (TOS) |VCM_TOS |60 |
||Torch Log Service (TLS) |VCM_TLS |30 |
|Middleware |Bytedance Message Queue (BMQ) |VCM_BMQ |30 |
||Cloud Search |VCM_ESCloud |30 |
||Cloud Search Serverless |VCM_ESCloud_Serverless |30 |
||Configuration Center \- Etcd |VCM_ConfigCenter_Etcd |30 |
||Configuration Center \- Zookeeper |VCM_ConfigCenter_ZooKeeper |30 |
||Vital Managed Service for Prometheus |VCM_Prometheus |30 |
||Message Queue for Kafka |VCM_Kafka |30 |
||Message Queue for RabbitMQ |VCM_RabbitMQ |30 |
||Message Queue for RocketMQ |VCM_RocketMQ |30 |
|Network |Application Load Balancer (ALB) |VCM_ALB |60 |
||Anycast EIP |VCM_AnycastEIP |30 |
||Bandwidth Package |VCM_BandwidthPackage |30 |
||Cloud Enterprise Network (CEN) |VCM_CEN |30 |
||Classic Load Balancer (CLB) |VCM_CLB |60 |
||CLB dedicated cluster |VCM_CLB_EC |30 |
||Cloud Connector (CC) |VCM_CloudConnector |30 |
||Direct Connect (DC) \- DC connection |VCM_DirectConnectConnection |30 |
||Direct Connect (DC) \- DC gateway |VCM_DirectConnectGateway |30 |
||DC \- virtual interface |VCM_DirectConnectVIF |30 |
||Elastic IP (EIP) |VCM_EIP |60 |
||Internet Express |VCM_Fasttrack |30 |
||IPsec\-VPN connection |VCM_IPsec |30 |
||Internet Channel \- Public Bandwidth |VCM_InternetTunnelBandwidth |30 |
||Internet Channel Virtual Interface |VCM_InternetTunnelVirtualInterface |30 |
||Vortex IP |VCM_Vortex_IP |30 |
||Byte Interconnection Service \- Network |VCM_BIS |30 |
||IPv6 Internet bandwidth |VCM_Ipv6AddressBandwidth |30 |
||IPv6 Gateway (IPv6GW) |VCM_Ipv6Gateway |30 |
||NAT Gateway |VCM_NAT |30 |
||NAT64 gateway |VCM_NAT64 |30 |
||Private Link \- endpoint |VCM_PrivateLinkEndpoint |30 |
||Private Link \- endpoint service |VCM_PrivateLinkEndpointService |30 |
||Private Link \- Private Link gateway |VCM_PrivateLinkGateway |30 |
||Private NAT Gateway |VCM_PrivateNAT |30 |
||TR |VCM_TransitRouter |30 |
||Transit Router (TR) Bandwidth Package |VCM_TransitRouterBandwidthPackage |30 |
||VPN connection |VCM_VPN |30 |
|Data middleend |ByteHouse CDW |VCM_ByteHouse |30 |
||ByteHouse CE |VCM_ByteHouse_Ce |30 |
||ByteHouse CDW \- data importing |VCM_ByteHouse_DataLoading |30 |
||DataLeap |VCM_DataLeap |30 |
||DataSail |VCM_DataSail |30 |
||DataSail \- object group |VCM_DataSail_ResourceGroup |30 |
||DataSail \- collection topic |VCM_DataSail_Topic |30 |
||E\-MapReduce |VCM_EMR |30 |
||E\-MapReduce on VKE |VCM_EMR_ON_VKE |30 |
||E\-MapReduce (EMR) StarRocks |VCM_EMR_StarRocks |30 |
||Stream Computing Flink Edition |VCM_Flink |30 |
||Batch computing Spark edition |VCM_Spark |30 |
||Lakehouse Analytics Service (LAS) |VCM_LAS |30 |
|Security |Advanced DDoS Protection |VCM_Adv_DDoS_Protection |30 |
||Advanced DDoS Protection \- Domain |VCM_Adv_DDoS_Protection_Domain |30 |
|R&D middleend |Internet of Things Platform |VCM_IoT |30 |
|Artificial intelligence and algorithms |VikingDB |VCM_VikingDB |30 |
|Domain names and websites |TrafficRoute \- HTTPDNS |VCM_TrafficRoute_HTTPDNS |30 |
