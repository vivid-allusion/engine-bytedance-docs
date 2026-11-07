---
title: "Connecting to a cluster using cURL"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-cURL"
---

An ES instance provides a private endpoint by default. You can log on to an Elastic Compute Service (ECS) instance in the same virtual private cloud (VPC) as the ES instance and run cURL commands to access the ES instance. This topic describes how to connect to a Cloud Search instance by using cURL commands and provides examples of simple operations.

<span id="ca99d74e"></span>
## Accessing a Cloud Search instance


1. Log on to an ECS instance in the same VPC as your Cloud Search instance. For more information, refer to [Logging on to ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command on the ECS instance to access the Cloud Search instance.

   * Accessing an HTTP protocol instance

      ```Plain
      curl -u <user>:<password> <host>
      ```
      

   * Accessing an HTTPS protocol instance

      For an HTTPS protocol instance, to get quick access, add the  **`-k`** or  **`--insecure`** parameter to the cURL command to disable certificate verification.

      ```JSON
      curl -k -u <user>:<password> <host>
      ```
      

      
      |**Variable** |**Description** |
      |---|---|
      |user |The username used to log on to the instance. The default value is admin. |
      |password |The password used to log on to the instance. |
      |host |The private or public endpoint of the instance. You can get this endpoint on the **Instance information** page. |
      

   Example:

   ```Shell
   # ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
   curl -k -u : https://elasticsearch-o-00w**93s1.escloud.ibytepluses.com:9200
   ```
   

   If information similar to the following is returned, the instance can be accessed normally. The return values vary based on the instance version.

   ```JSON
   {
     "name" : "es-master-00**3s1-2",
     "cluster_name" : "00**3s1",
     "cluster_uuid" : "ocvwXJT**KAbAw",
     "version" : {
       "number" : "7.10.2",
       "build_flavor" : "default",
       "build_type" : "tar",
       "build_hash" : "747e1cc71def077*a59143c1f785afa92b9",
       "build_date" : "2021-01-13T00:42:12.435326Z",
       "build_snapshot" : false,
       "lucene_version" : "8.7.0",
       "minimum_wire_compatibility_version" : "6.8.0",
       "minimum_index_compatibility_version" : "6.0.0-beta1"
     },
     "tagline" : "You Know, for Search"
   } 
   ```
   


<span id="55e45a20"></span>
## Creating documents

<span id="2c28ce2d"></span>
### Creating a single document

Run the following command to create an index named `customer` and add a document whose `id` is 1 to the index.

```Shell
# ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
curl -XPUT -u admin:password http://192.168.*.*:9200/customer/_doc/1 -H 'Content-Type: application/json' -d '
{
  "name": "Alice",
  "address":"Wuhou District, Chengdu City, Sichuan Province",
  "city":"Chengdu",
  "age":28,
  "birthday":"1993-08-30",
  "level.viplevel":3,
  "level.viptype":"Premium VIP"
}
'
```


The following information is returned:

```JSON
{
"_index":"customer",
"_type":"_doc",
"_id":"1",
"_version":1,
"result":"created",
"_shards":{
    "total":2,
    "successful":1,
    "failed":0
},
"created":true
}
```


<span id="0bed986f"></span>
### Creating multiple documents

Run the following command to add multiple documents to an index at a time.

```Shell
# ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
curl -XPOST -u admin:P_ssw0rd http://192.168.*.*:9200/_bulk -H 'Content-Type: application/json' -d '
{"index" : { "_index": "customer","_id":2} }
{"name":"Tom","address":"Haidian District","city":"Beijing","age":"23","birthday":"1998-01-01","level":{"viplevel":3,"viptype":"Premium VIP"}}
{"index" : { "_index": "customer","_id":3} }
{"name":"Joe","address":"Binjiang District, Hangzhou City, Zhejiang Province","city":"Hangzhou","age":"30","birthday":"1991-05-05","level":{"viplevel":5,"viptype":"Diamond VIP"}}
'
```


The following information is returned:

```JSON
{"took":15,"errors":false,"items":[{"index":{"_index":"customer","_type":"_doc","_id":"2","_version":2,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":6,"_primary_term":1,"status":200}},{"index":{"_index":"customer","_type":"_doc","_id":"3","_version":2,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":7,"_primary_term":1,"status":200}}]}
```


<span id="6a437232"></span>
## Querying documents

<span id="45bea3d2"></span>
### Querying a document with a specified ID

```Shell
curl -XGET -u admin:P_ssw0rd  'http://192.168.*.*:9200/customer/_doc/1?pretty' -H 'Content-Type: application/json'
```


The following information is returned:

```JSON
{
  "_index" : "customer",
  "_type" : "_doc",
  "_id" : "1",
  "_version" : 6,
  "_seq_no" : 9,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "name" : "Alice",
    "address" : "Wuhou District, Chengdu City, Sichuan Province",
    "city" : "Chengdu",
    "age" : 28,
    "birthday" : "1993-08-30",
    "level.viplevel" : 3,
    "level.viptype" : "Premium VIP"
  }
}
```


<span id="4a8e6275"></span>
### Querying all documents

```Shell
curl -XGET -u admin:P_ssw0rd  'https://192.168.*.*:9200/customer/_doc/_search?pretty' -H 'Content-Type: application/json' 
```


The following information is returned:

```JSON
{
  "took" : 5,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 3,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "customer",
        "_type" : "_doc",
        "_id" : "2",
        "_score" : 1.0,
        "_source" : {
          "name" : "Tom",
          "address" : "Haidian District",
          "city" : "Beijing",
          "age" : "23",
          "birthday" : "1998-01-01",
          "level" : {
            "viplevel" : 3,
            "viptype" : "Premium VIP"
          }
        }
      },
      {
        "_index" : "customer",
        "_type" : "_doc",
        "_id" : "3",
        "_score" : 1.0,
        "_source" : {
          "name" : "Joe",
          "address" : "Binjiang District, Hangzhou City, Zhejiang Province",
          "city" : "Hangzhou",
          "age" : "30",
          "birthday" : "1991-05-05",
          "level" : {
            "viplevel" : 5,
            "viptype" : "Diamond VIP"
          }
        }
      },
      {
        "_index" : "customer",
        "_type" : "_doc",
        "_id" : "1",
        "_score" : 1.0,
        "_source" : {
          "name" : "Alice",
          "address" : "Wuhou District, Chengdu City, Sichuan Province",
          "city" : "Chengdu",
          "age" : 28,
          "birthday" : "1993-08-30",
          "level.viplevel" : 3,
          "level.viptype" : "Premium VIP"
        }
      }
    ]
  }
} 
```
