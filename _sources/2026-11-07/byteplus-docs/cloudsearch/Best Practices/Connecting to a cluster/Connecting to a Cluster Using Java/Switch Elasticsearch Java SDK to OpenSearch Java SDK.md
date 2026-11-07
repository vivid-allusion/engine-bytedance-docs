---
title: "Switch Elasticsearch Java SDK to OpenSearch Java SDK"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Switch_Elasticsearch_Java_SDK_to_OpenSearch_Java_SDK"
---

Cloud Search currently supports Elasticsearch 7.10.2 and later versions and OpenSearch 2.9.0 and later version instances. If switching from an Elasticsearch 7.10.2 or later instance to an OpenSearch 2.9.0 or later instance, you must switch to the OpenSearch 2.9 or later Java SDK to connect to the instance using the Java SDK. This article uses the Java High Level REST Client as an example to explain the SDK switching process.

<span id="29541528"></span>
## Background

OpenSearch 2.9.0 and later SDKs are basically compatible with Elasticsearch 7.10.2 and later x\-pack\-excluded APIs, meaning compatible with Elasticsearch 7.10.2 OSS APIs. To switch SDK normally, users only need to make the following three changes:


1. Modify the Maven `pom.xml` or Gradle `build.gradle` file.

2. Modify the import paths of related packages in the source code.

3. Upgrade the JDK version. Elasticsearch 7.10.2 and later require at least JDK 1.8, while OpenSearch 2.9.0 and later require at least JDK 11.


<span id="ff4cfd44"></span>
## Prepare the environment


1. Prepare test data.

   The test data comes from the Elasticsearch OSS repository [accounts.json](https://github.com/elastic/elasticsearch/blob/v7.10.2/docs/src/test/resources/accounts.json).

2. Use the following command to index the test data into the Elasticsearch instance.

   If you need to index data into OpenSearch, the import command is the same.

   ```JSON
   curl -k -XPOST -u <user>:<password>  -H "Content-Type: application/x-ndjson" https://localhost:9200/accounts/_bulk --data-binary @accounts.json
   ```
   


<span id="acd6e508"></span>
## Elasticsearch SDK

This section mainly introduces the usage of the Elasticsearch 7.10.2 Java High Level REST Client SDK.


1. Add the ES SDK dependency declaration in the `build.gradle` build file.

   ```Groovy
   dependencies {
       implementation 'org.elasticsearch.client:elasticsearch-rest-high-level-client:7.10.2'
       ....
   }
   ```
   

2. Query usage.

   ```Java
   import org.apache.http.HttpHost;
   import org.apache.http.auth.AuthScope;
   import org.apache.http.auth.UsernamePasswordCredentials;
   import org.apache.http.client.CredentialsProvider;
   import org.apache.http.conn.ssl.NoopHostnameVerifier;
   import org.apache.http.conn.ssl.TrustAllStrategy;
   import org.apache.http.impl.client.BasicCredentialsProvider;
   import org.apache.http.ssl.SSLContexts;
   import org.elasticsearch.action.search.SearchRequest;
   import org.elasticsearch.action.search.SearchResponse;
   import org.elasticsearch.client.RequestOptions;
   import org.elasticsearch.client.RestClient;
   import org.elasticsearch.client.RestHighLevelClient;
   import org.elasticsearch.index.query.QueryBuilder;
   import org.elasticsearch.index.query.QueryBuilders;
   import org.elasticsearch.search.builder.SearchSourceBuilder;
   
   import javax.net.ssl.SSLContext;
   import java.io.IOException;
   import java.security.KeyManagementException;
   import java.security.KeyStoreException;
   import java.security.NoSuchAlgorithmException;
   
   public class Main {
       private static RestHighLevelClient client;
       public static void main(String[] args) throws IOException, NoSuchAlgorithmException, KeyStoreException, KeyManagementException {
           initEsClient();
           try {
               QueryBuilder query = QueryBuilders.matchQuery("city", "Vernon");
               SearchSourceBuilder sourceBuilder = new SearchSourceBuilder()
                   .size(1000)
                   .query(query);
               SearchRequest searchRequest = new SearchRequest()
                   .indices("accounts")
                   .source(sourceBuilder);
   
               SearchResponse response = client.search(searchRequest, RequestOptions.DEFAULT);
               System.out.println(response.getHits().getHits()[0].getId());
           } finally {
               client.close();
           }
       }
   
       private static void initEsClient() throws NoSuchAlgorithmException, KeyStoreException, KeyManagementException {
         // Ignore
       }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Ignore part in the above Java code needs to be replaced with an initialization statement. You can refer to <a href="https://docs.byteplus.com/docs/cloudsearch/connecting-cluster-Java">connecting to an ES instance by Java</a>.   </div>
   

<span id="e2526639"></span>
## Switch to OpenSearch 2.9.0 SDK


1. Modify the SDK dependency declaration in the `build.gradle` build file, replacing the Elasticsearch SDK with the OpenSearch 2.9.0 SDK.

   ```Java
   dependencies {
       implementation 'org.opensearch.client:opensearch-rest-high-level-client:2.9.0'
       ....
   }
   ```
   

2. Only modify the import package <a i=1\>path</a\> in the source files; no other changes are needed.

   
   |**Original import statements** |**Modified import statements** |
   |---|---|
   |```Java```<br>```import org.elasticsearch.action.search.SearchRequest;```<br>```import org.elasticsearch.action.search.SearchResponse;```<br>```import org.elasticsearch.client.RequestOptions;```<br>```import org.elasticsearch.client.RestClient;```<br>```import org.elasticsearch.client.RestHighLevelClient;```<br>```import org.elasticsearch.index.query.QueryBuilder;```<br>```import org.elasticsearch.index.query.QueryBuilders;```<br>```import org.elasticsearch.search.builder.SearchSourceBuilder;```<br> |```Java```<br>```import org.opensearch.action.search.SearchRequest;```<br>```import org.opensearch.action.search.SearchResponse;```<br>```import org.opensearch.client.RequestOptions;```<br>```import org.opensearch.client.RestClient;```<br>```import org.opensearch.client.RestHighLevelClient;```<br>```import org.opensearch.index.query.QueryBuilder;```<br>```import org.opensearch.index.query.QueryBuilders;```<br>```import org.opensearch.search.builder.SearchSourceBuilder;```<br> |
