---
title: "Prometheus configuration for fully managed OLAP cluster solution"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Prometheus_configuration_for_fully_managed_OLAP_cluster_solution"
---

<span id="b12b010d"></span>
## Prerequisites


1. EMR Serverless instance has been created.

2. ECS has been created in the same VPC, and Prometheus has been installed. Installation method:


```PowerShell
# 华北prometheus内网下载地址
wget https://emr-autotest.tos-cn-beijing.ivolces.com/prometheus-2.29.1.linux-amd64.tar.gz

tar -zxvf prometheus-2.29.1.linux-amd64.tar.gz
cd prometheus-2.29.1.linux-amd64
mkdir /data01/prometheus-data

./prometheus --web.enable-lifecycle --config.file="/root/prometheus-2.29.1.linux-amd64/prometheus.yml" --storage.tsdb.path="/data01/prometheus-data" --storage.tsdb.retention.time=5d &
```


<span id="38c8cb36"></span>
## Procedure


1. Obtain the FE and BE node addresses in the instance.

   1. To obtain the addresses from the page: Go to **EMR Serverless Console \> Instance \> Network Connection**, and click **View All Nodes** in the upper right corner.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfb98de6e70a4f6d9d845b2e322d427b~tplv-goo7wpa0wc-image.image) </span>

   2. To obtain the addresses from the command:

      ```SQL
      MYSQL_HOST="<IP_adress>" -- Host address of the server
      MYSQL_PORT="<MySQL协议端口>" -- The default port for the MySQL protocol is 9030
      MYSQL_USER="<Username>"
      MYSQL_PASSWORD="<Password>"
      mysql -h $MYSQL_HOST -P$MYSQL_PORT -u$MYSQL_USER -p$MYSQL_PASSWORD
      
      -- Obtain the list of FE nodes
      show frontends;
      
      -- Obtain the list of BE nodes
      show backends;
      
      -- Storage and compute separation
      show compute nodes;
      ```
      

2. Configure Prometheus.

   1. Open the Prometheus configuration file.

      ```PowerShell
      # Configure the Prometheus configuration. The configuration file path needs to be adjusted according to actual conditions
      vim /root/prometheus-2.29.1.linux-amd64/prometheus.yml
      ```
      

   2. Add the following configuration at the bottom of the YAML file and save it.

      ```YAML
       - job_name: 'cdw-3f5rji288d3niqkgdob6-baseline'
          metrics_path: '/metrics'
          static_configs:
          # FE node address
          - targets: ['192.168.16.74:8030']  
            labels:
              group: fe
          # BE/CN/warehouse node address
          - targets: ['192.168.28.218:8040', '192.168.16.105:8040', '192.168.16.103:8040']
            labels:
              group: be
      ```
      

   3. Reload the configuration file.

      ```PowerShell
      curl -X POST http://localhost:9090/-/reload
      ```
