---
title: "Traffic Mirror analysis example"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-analysis-example"
---

## Application scenarios

This topic introduces how to analyze traffic from Traffic Mirror.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34d40a119ca6b829723a8c656a08437c.png)

|Applications |Description of functions in this example |Related documents |
|---|---|---|
|Suricata |Decapsulate the traffic mirror data from VXLAN encapsulation. |[What is Suricata](https://docs.suricata.io/en/latest/what-is-suricata.html) |
|Filebeat |Collect log data and forward it to Elasticsearch. |[Filebeat overview](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html) |
|Elasticsearch |Store data and provide search indexing. |[What is Elasticsearch?](https://www.elastic.co/guide/en/elasticsearch/reference/8.17/elasticsearch-intro-what-is-es.html) |
|Kibana |Analyze and visualize the data in Elasticsearch. |[What is Kibana?](https://www.elastic.co/guide/en/kibana/8.17/introduction.html) |

> **tip**

> All the software mentioned above is open\-source. You may also choose other analysis tools.

## Prerequisites

1. The steps in the [Traffic Mirror Getting started](https://docs.byteplus.com/en/docs/vpc/Traffic-Mirror-Quick-start) have been completed.

2. Within the same VPC, two additional ECSs—ECS\-Elasticsearch and ECS\-Kibana—have been added, each bound to an EIP.

3. Allow TCP traffic from the CIDR range 0.0.0.0/0 on port 5601 in the inbound security group rules associated with ECS\-Kibana. For instructions, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

   > **Tip**

   * > **Security Warning**: Kibana uses the elastic superuser account for login. If port 5601 is open to 0.0.0.0/0, the management console will be exposed directly to the public internet, making it vulnerable to brute\-force attacks and unauthorized access. The 0.0.0.0/0 rule shown in this guide is for a demo environment only. Do not replicate this configuration in production.

   * > **Recommendation**: Restrict the source IP to your admin public IP, or access Kibana via VPN / bastion host.

## Procedures

> **tip**

> All ECSs in this topic use CentOS 7.9 as an example.

### Step 1: Install Suricata

1. Log in to the ECS\-TrafficMirrorTarget.

2. Run the following commands sequentially to install Suricata.

   ```JSON
   sudo yum install epel-release yum-plugin-copr
   sudo yum copr enable @oisf/suricata-7.0
   sudo yum install suricata
   ```

3. Run the following command to start Suricata.

   ```Shell
   sudo systemctl enable suricata
   sudo systemctl start suricata
   ```

4. Execute the following command to view the **Log file**.

   ```Bash
   cd /var/log/suricata
   ls
   ```

   The log file is shown in the figure below.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c48f0a2bac9d33de6a8828619a5d746.png)

### Step 2: Install Elasticsearch

You can refer to this procedure to install an Elasticsearch node.

1. Log in to the ECS\-Elasticsearch.

2. Execute the following command to create and switch to the `elastic-install-files` directory.

   ```JSON
   mkdir elastic-install-files
   cd elastic-install-files
   ```

3. Run the following command to download Elasticsearch.

   `wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.17.2-x86_64.rpm`

4. Run the following command to install Elasticsearch.

   `sudo rpm --install elasticsearch-8.17.2-x86_64.rpm`

   During Elasticsearch installation, the following security features are enabled by default:

   * Authentication and authorization are enabled, including a built\-in elastic superuser account.

   * TLS (Transport Layer Security) certificates and keys are generated for both the transport layer and the HTTP layer, and TLS is enabled and configured using these keys and certificates.

5. Copy the terminal output of the installation command to a local file. Especially the **Password of the elastic super user account**.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_00f8b78e826c3747821b5c594510c75a.png)

6. Execute the following command to configure Elasticsearch to start automatically on boot.

   ```Bash
   sudo systemctl daemon-reload
   sudo systemctl enable elasticsearch.service
   ```

7. Open `sudo vim /etc/elasticsearch/elasticsearch.yml `configuration file and configure it as follows.

   ```Bash
   # ---------------------------------- Cluster -----------------------------------
   cluster.name: elasticsearch-demo # In a multi-node Elasticsearch cluster, all Elasticsearch instances must have the same cluster name.
   
   # ---------------------------------- Network -----------------------------------
   network.host: 192.168.1.4 # IP address of ECS-Elasticsearch
   http.port: 9200
   
   #----------------------- BEGIN SECURITY AUTO CONFIGURATION -----------------------
   transport.host: 0.0.0.0 # The setting 0.0.0.0 allows Elasticsearch to listen for connections on all available network interfaces. You can also restrict the listening scope by setting this value to match the value configured for network.host.
   ```

   Save changes and disable the editor.

8. Execute the following command to start Elasticsearch.

   `sudo systemctl start elasticsearch.service`

   > If needed, you can stop the service by running `sudo systemctl stop elasticsearch.service`.

   9. Ensure that Elasticsearch is running normally.

   `sudo curl --cacert /etc/elasticsearch/certs/http_ca.crt -u elastic:$ELASTIC_PASSWORD https://localhost:9200`

   Example: sudo curl \-\-cacert /etc/elasticsearch/certs/http_ca.crt \-u elastic: _Nf0\*\*\*\*LRp7 https://localhost:9200

tip

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fad024bbc9486f012fddb957f8ca0e4c.png)

   Replace `$ELASTIC_PASSWORD` with the **Elastic superuser password** you copied during the Elasticsearch installation.

10. Run the following command to check the status of Elasticsearch.

   `sudo systemctl status elasticsearch`

### Step 3: Install Kibana

1. Log in to the ECS\-Kibana.

2. Run the following command to create and switch to the `kibana-install-files` directory.

   ```JSON
   mkdir kibana-install-files
   cd kibana-install-files
   ```

3. Run the following command to download the Kibana installation package.

   `wget https://artifacts.elastic.co/downloads/kibana/kibana-8.17.2-x86_64.rpm`

4. Run the following command to install Kibana.

   `sudo rpm --install kibana-8.17.2-x86_64.rpm`

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53b973112877df48498e10c057ad2954.png)

5. Switch to ECS\-Elasticsearch and execute the following command to generate the enrollment token required for Kibana to connect to Elasticsearch.

   `sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana`

   > Copy the generated enrollment token from the command output.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c1e7b0f51d6b8ae70afa79d591befbd.png)

   `Example: eyJ2ZXIiOiI4LjE0LjAiLCJhZHIiOlsiMTkyLjE2OC4xLjQ6OTIwMCJdLCJmZ3IiOiJhMWY1YzQ2Njg5ZDI0YWRlYjdjZTg0ZDc2MjA2YmM1MmE4NzMwZDIxYTg4MGNlMzM1MGM1YjIwYWRjMjAyN2*****`

6. Run the following two commands to configure Kibana to start automatically on boot.

   ```JSON
   sudo systemctl daemon-reload
   sudo systemctl enable kibana.service
   ```

7. Open the `sudo vim /etc/kibana/kibana.yml` configuration file and configure the following information:

   ```Bash
   #=================== System: Kibana Server ===================
   server.port: 5601
   server.host: "192.168.1.5" # IP address of ECS-Kibana
   ```

   Save changes and disable editor.

8. Run the following command to start the Kibana service:

   `sudo systemctl start kibana.service`

   > If needed, you can stop the service by running `sudo systemctl stop kibana.service`.

9. Run the following command to check the status of Kibana.

   `sudo systemctl status kibana`

10. In the local computer's browser, input `http://< kibana's Elastic IP >: 5601`.

11. Input the token previously generated in ECS\-Elasticsearch and click **Configure Elastic**.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ddd52cac4c4d61f4b55c8c6e07048e83.png)

   > **warning**

   * > If you are unable to connect, please check whether the inbound rules of the security group associated with ECS\-Kibana allow traffic with the TCP protocol, from the CIDR block 0.0.0.0/0, and on port 5601.

   * > The token generated by Elasticsearch for the Elastic Compute Service expires if not used within 30 minutes. If it has expired, please regenerate it.

12. **Enter the verification code.**

   In ECS\-Kibana, execute` sudo systemctl status kibana` to obtain a 6\-digit verification code **.**

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d2135a13163f1d250fdfa1a841f46fb.png)

13. Input the username and password, the username is **elastic**, and the password is the Password output by ECS\-Elasticsearch when installed on the terminal. For example, `_Nf0****LRp7`.

14. Click **Log in**. You will be successfully logged in.

Kibana has been successfully configured and is now communicating with Elasticsearch.

### Step 4: Install Filebeat

1. Log in to the ECS\-TrafficMirrorTarget.

2. Execute the following command to create and switch to the Filebeat\-install\-files directory.

   ```JSON
   mkdir Filebeat-install-files
   cd Filebeat-install-files
   ```

3. Execute the following command to download and unzip the Filebeat installation package.

   ```JSON
   curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.17.2-linux-x86_64.tar.gz
   tar -xzvf filebeat-8.17.2-linux-x86_64.tar.gz
   ```

4. Switch to the ECS\-Elasticsearch, execute the following command to get the `ca_trusted_fingerprint` value from the `filebeat.yml` file.

   `openssl x509 -fingerprint -sha256 -noout -in /etc/elasticsearch/certs/http_ca.crt`

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8fe49f0dc39a3259efc481121fe61a8.png)

   Copy the return value to a local file, and remove the `:` symbols, e.g., `A1F5C46689D24ADEB7CE84D76206BC52A8730D21A880CE3350C5B20ADC2027D3`

5. Switch to the ECS\-TrafficMirrorTarget, enter the Filebeat installation package directory, open the filebeat.yml file, and configure the connection information for Elasticsearch and Kibana.

      ```Bash
      # =================================== Kibana ===================================
      setup.kibana: 
         host: "192.168.1.5:5601"  # Set to the IP address of your Kibana instance
         username: "elastic"   
         password: "_Nf0****LRp7" # This topic sets it to the registration password of Elasticsearch
      
      # ---------------------------- Elasticsearch Output ----------------------------
      output.elasticsearch: 
        hosts: ["192.168.1.4:9200"] # Set the IP Address for elasticsearch
        protocol: "https" # Set to HTTPS
        username: "elastic" 
        password: "_Nf0****LRp7" # Set the registration password for elasticsearch
        ssl: 
          enabled: true 
          ca_trusted_fingerprint: "A1F5C46689D24ADEB7CE84D76206BC52A8730D21A880CE3350C5B20ADC2027D3" 
          # Value for ca_trusted_fingerprint: On ECS-Elasticsearch, run the command [openssl x509 -fingerprint -sha256 -noout -in /etc/elasticsearch/certs/http_ca.crt], take the output result [xx:xx:xx:xx] and remove the colons
      ```

6. Execute the following command to view the available modules in Filebeat and confirm whether the `Suricata` module is available.

   `./filebeat modules list`

7. Run the following command to enable the `Suricata` module.

   `./filebeat modules enable suricata`

8. Switch to the `modules.d` directory, open the `suricata.yml` file, and configure the following information.

   ```Bash
   - module: suricata
     eve:
       enabled: true
       var.paths: ["/var/log/suricata/eve*"] # This path is the log directory for Suricata.
   ```

9. Switch to the directory where the Filebeat binary is installed and run Filebeat.

   ```Bash
   cd ..
   ./filebeat test config -e
   ```

10. Run the following command to set up assets. The process is expected to take approximately 3 minutes. Please wait patiently.

   `./filebeat setup -e`

11. Run the following command to start Filebeat.

   ```Bash
   sudo chown root filebeat.yml 
   sudo chown root modules.d/suricata.yml 
   sudo ./filebeat -e 
   ```

## Verification

1. Enter `http://<kibana's Elastic IP>:5601` in your local computer's browser.

2. Enter your account and password.

3. In the left\-side navigation pane, select **Discover** and input commands as needed for analysis.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92cbcfb482d5aef45a72b89f731418f2.png)
