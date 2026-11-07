---
title: "Connecting to a cluster using Java"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-Java"
---

Open source Elasticsearch and the community have rolled out SDKs in various programming languages for your convenience. This topic describes how to connect to an ES instance by using the Java High Level REST Client and provides you with sample code.

<span id="6b90ea3a"></span>
## Preparation


* Create an ES instance and make sure that it runs normally. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).

* Get the instance endpoint and user information that are used to access the instance on the **Basic information** page. For an HTTPS protocol instance that requires certificate verification, you must also download the certificate and save it to a local path.

   * You can reset the password if you forget the password of the user (admin) accessing the instance.

   * If you want to access the instance by using the public endpoint, enable internet\-facing access to the instance and then associate the instance with an elastic IP address (EIP).

* Install a Java environment on the server that runs Java code. The Java Development Kit (JDK) version must be 1.8 or later. In addition, install Maven 3.5 or later versions. For more information, refer to [Installing a JDK](https://www.oracle.com/java/technologies/javase-downloads.html) and [Installing Maven](http://maven.apache.org/download.cgi#).

* Make sure that the server running Java code can communicate with the ES instance.

   * If the server running Java code is in the same virtual private cloud (VPC) as the ES instance, the ES instance can be connected using its private endpoint.

   * If the server running Java code is in the internet environment, the Cloud Search instance can be connected using its public endpoint. For more information, refer to [Enabling public network access to an instance](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access).


<span id="eec4a2da"></span>
## Precautions

We recommend that you use a Rest High Level Client whose version is consistent with that of the ES instance. If you use a Rest High Level Client whose version is later than that of the ES instance, compatibility issues may occur in a small number of requests.

For example, if the version of the ES instance you want to access is 7.10.2, install Rest High Level Client version 7.10.2.

<span id="2544b6bd"></span>
## Adding dependencies

Add the following dependencies to the `pom.xml` file. Specify the versions of the ES instance and the Rest High Level Client as needed. In this example, version 7.10.2 is used.

```XML
<dependency>
    <groupId>org.elasticsearchgroupId>
    <artifactId>elasticsearchartifactId>
    <version>7.10.2version>
dependency>

<dependency>
    <groupId>org.elasticsearch.clientgroupId>
    <artifactId>elasticsearch-rest-clientartifactId>
    <version>7.10.2version>
dependency>

<dependency>
    <groupId>org.elasticsearch.clientgroupId>
    <artifactId>elasticsearch-rest-high-level-clientartifactId>
    <version>7.10.2version>
dependency>

<dependency>
    <groupId>org.projectlombokgroupId>
    <artifactId>lombokartifactId>
    <version>0.10.1version>
    <scope>providedscope>
dependency>

<dependency>
    <groupId>org.springframeworkgroupId>
    <artifactId>spring-contextartifactId>
    <version>5.3.9version>
dependency>
```


<span id="8b900a6d"></span>
## Connecting to the cluster with certificate verification

This scenario applies to ES instances that must be connected over HTTPS and require HTTPS certificate verification during the connection process.

Sample code:

```Java
package com.bytedance.openplatform.imgr.core.client;

import java.io.IOException;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.security.KeyStore;
import java.security.cert.Certificate;
import java.security.cert.CertificateFactory;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.concurrent.TimeUnit;
import javax.net.ssl.SSLContext;
import lombok.extern.slf4j.Slf4j;
import org.apache.http.HttpHost;
import org.apache.http.auth.AuthScope;
import org.apache.http.auth.UsernamePasswordCredentials;
import org.apache.http.client.CredentialsProvider;
import org.apache.http.conn.ssl.NoopHostnameVerifier;
import org.apache.http.impl.client.BasicCredentialsProvider;
import org.apache.http.impl.nio.reactor.IOReactorConfig;
import org.apache.http.nio.conn.ssl.SSLIOSessionStrategy;
import org.apache.http.ssl.SSLContextBuilder;
import org.apache.http.ssl.SSLContexts;
import org.elasticsearch.action.admin.cluster.health.ClusterHealthRequest;
import org.elasticsearch.action.admin.cluster.health.ClusterHealthResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestClientBuilder;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.common.settings.Settings;
import org.springframework.stereotype.Component;


/**
 * Connect to the HTTPS cluster by using a Rest Hive Level Client with certificate verification.
 */

public class ESClient {

    RestHighLevelClient initClientWithCA(List hosts, int port, String protocol, String caPath, String user, String password) throws Exception {
        HttpHost[] httpHosts = hosts.stream().map(host -> new HttpHost(host, port, protocol)).toArray(HttpHost[]::new);
        RestClientBuilder restClientBuilder = RestClient.builder(httpHosts);
        CredentialsProvider provider = new BasicCredentialsProvider();
        provider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(user, password));
        InputStream is = Files.newInputStream(Paths.get(caPath));
        CertificateFactory factory = CertificateFactory.getInstance("X.509");
        Certificate trustedCa = factory.generateCertificate(is);
        KeyStore trustStore = KeyStore.getInstance("pkcs12");
        trustStore.load(null, null);
        trustStore.setCertificateEntry("ca", trustedCa);
        SSLContextBuilder sslContextBuilder = SSLContexts.custom()
                .loadTrustMaterial(trustStore, null);
        SSLContext sslContext = sslContextBuilder.build();
        restClientBuilder.setHttpClientConfigCallback(httpClientBuilder -> {
            httpClientBuilder.setDefaultCredentialsProvider(provider)
                    .setDefaultIOReactorConfig(IOReactorConfig.custom().setSoKeepAlive(true).build())
                    //keepalive
                    .setKeepAliveStrategy((httpResponse, httpContext) -> TimeUnit.MINUTES.toMillis(2))
                    .setSSLStrategy(new SSLIOSessionStrategy(sslContext, NoopHostnameVerifier.INSTANCE));
            return httpClientBuilder;
        });
        // Set the related timeout period.
        restClientBuilder.setRequestConfigCallback(builder -> builder
                .setConnectionRequestTimeout(5000)
                .setSocketTimeout(60000)
                .setConnectTimeout(5000));
        return new RestHighLevelClient(restClientBuilder);
    }

    // Specify the endpoint of the ES cluster, logon user, and HTTPS certificate information.
   public static void main(String[] args) throws Exception {
        ESClient esClientBak = new ESClient();
       RestHighLevelClient restHighLevelClient = esClientBak.initClientWithCA(
                Arrays.asList("{INSTANCE_CONN_ADDR}"), 9200,
               "https", "{CERT_STORAGE_Path}",
               "{INSTANCE_USER}", "{PASSWORD}");
        ClusterHealthRequest request = new ClusterHealthRequest();
        try {
            ClusterHealthResponse health = restHighLevelClient.cluster().health(request, RequestOptions.DEFAULT);
        } catch (IOException e) {
           e.printStackTrace();
        }

       /**
        * Create an index.
        */
       // Create an index and set the index name, number of allocated shards, and number of replicas.
       CreateIndexRequest createIndexRequest = new CreateIndexRequest("{INDEX_NAME}");
       createIndexRequest.settings(Settings.builder()
               .put("index.number_of_shards", 3)
               .put("index.number_of_replicas", 1));

       // Set the mapping for the index and configure fields as needed.
       HashMap properties = new HashMap();
       properties.put("name",
               Collections.singletonMap("type", "keyword"));
       properties.put("age",
               Collections.singletonMap("type", "integer"));

       HashMap mapping = new HashMap();
       mapping.put("properties", properties);

       createIndexRequest.mapping(mapping);

       // Create an index request.
       CreateIndexResponse createIndexResponse = restHighLevelClient.indices()
               .create(createIndexRequest, RequestOptions.DEFAULT);
       System.out.println("isAcknowledged=" + createIndexResponse.isAcknowledged() +
               "\nshards_acknowledged=" + createIndexResponse.isShardsAcknowledged() +
               "\nindex=" + createIndexResponse.index());
       restHighLevelClient.close();
   }

}
```


Run the program. Information similar to the following is returned:

```JSON
isAcknowledged=true
shards_acknowledged=true
index=custom-index
```


<span id="49aabbb0"></span>
## Connecting to the cluster without certificate verification

This scenario applies to ES instances that can be connected over HTTPS or HTTP and do not verify HTTPS certificates during the connection process.

Sample code:

```Java
package com.bytedance.openplatform.imgr.core.client;

import java.io.IOException;
import java.security.KeyManagementException;
import java.security.KeyStoreException;
import java.security.NoSuchAlgorithmException;
import java.util.Arrays;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.concurrent.TimeUnit;
import javax.net.ssl.SSLContext;
import lombok.extern.slf4j.Slf4j;
import org.apache.http.HttpHost;
import org.apache.http.auth.AuthScope;
import org.apache.http.auth.UsernamePasswordCredentials;
import org.apache.http.client.CredentialsProvider;
import org.apache.http.conn.ssl.NoopHostnameVerifier;
import org.apache.http.impl.client.BasicCredentialsProvider;
import org.apache.http.impl.nio.reactor.IOReactorConfig;
import org.apache.http.nio.conn.ssl.SSLIOSessionStrategy;
import org.apache.http.ssl.SSLContextBuilder;
import org.elasticsearch.action.admin.cluster.health.ClusterHealthRequest;
import org.elasticsearch.action.admin.cluster.health.ClusterHealthResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestClientBuilder;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.common.settings.Settings;
import org.springframework.stereotype.Component;


/**
 * Connect to the HTTPS cluster by using a Rest Hive Level Client without certificate verification.
 */

public class ESClient {

    RestHighLevelClient initClientSkipVerification(List hosts, int port, String protocol, String user, String password)
            throws NoSuchAlgorithmException, KeyStoreException, KeyManagementException {
        HttpHost[] httpHosts = hosts.stream().map(host -> new HttpHost(host, port, protocol)).toArray(HttpHost[]::new);
        RestClientBuilder restClientBuilder = RestClient.builder(httpHosts);
        CredentialsProvider provider = new BasicCredentialsProvider();
        provider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(user, password));
        SSLContext sslContext = new SSLContextBuilder().loadTrustMaterial(null, (x509Certificates, s) -> true).build();
        restClientBuilder.setHttpClientConfigCallback(httpClientBuilder -> {
            httpClientBuilder.setDefaultCredentialsProvider(provider)
                    .setDefaultIOReactorConfig(IOReactorConfig.custom().setSoKeepAlive(true).build())
                    //keepalive
                    .setKeepAliveStrategy((httpResponse, httpContext) -> TimeUnit.MINUTES.toMillis(2))
                    .setSSLStrategy(new SSLIOSessionStrategy(sslContext, NoopHostnameVerifier.INSTANCE));
            return httpClientBuilder;
        });
        // Set the related timeout period.
        restClientBuilder.setRequestConfigCallback(builder -> builder
                .setConnectionRequestTimeout(5000)
                .setSocketTimeout(60000)
                .setConnectTimeout(5000));
        return new RestHighLevelClient(restClientBuilder);
    }


    // Specify the endpoint of the ES cluster and the logon user.
   public static void main(String[] args) throws Exception {
        ESClient esClientBak = new ESClient();
       RestHighLevelClient restHighLevelClient = esClientBak.initClientSkipVerification(
                Arrays.asList("{INSTANCE_CONN_ADDR}"), 9200, "https",
               "{INSTANCE_USER}", "{PASSWORD}");
        ClusterHealthRequest request = new ClusterHealthRequest();
        try {
            ClusterHealthResponse health = restHighLevelClient.cluster().health(request, RequestOptions.DEFAULT);
        } catch (IOException e) {
           e.printStackTrace();
        }

       /**
        * Create an index.
        */
       // Create an index and set the index name, number of allocated shards, and number of replicas.
       CreateIndexRequest createIndexRequest = new CreateIndexRequest("{INDEX_NAME}");
       createIndexRequest.settings(Settings.builder()
               .put("index.number_of_shards", 3)
               .put("index.number_of_replicas", 1));

       // Set the mapping for the index and configure fields as needed.
       HashMap properties = new HashMap();
       properties.put("name",
               Collections.singletonMap("type", "keyword"));
       properties.put("age",
               Collections.singletonMap("type", "integer"));

       HashMap mapping = new HashMap();
       mapping.put("properties", properties);

       createIndexRequest.mapping(mapping);

       // Create an index request.
       CreateIndexResponse createIndexResponse = restHighLevelClient.indices()
               .create(createIndexRequest, RequestOptions.DEFAULT);
       System.out.println("isAcknowledged=" + createIndexResponse.isAcknowledged() +
               "\nshards_acknowledged=" + createIndexResponse.isShardsAcknowledged() +
               "\nindex=" + createIndexResponse.index());
       restHighLevelClient.close();
   }

}
```


Run the program. Information similar to the following is returned:

```JSON
isAcknowledged=true
shards_acknowledged=true
index=custom-index
```
