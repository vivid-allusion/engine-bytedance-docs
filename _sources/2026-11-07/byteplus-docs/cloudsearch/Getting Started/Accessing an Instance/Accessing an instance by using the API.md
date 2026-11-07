---
title: "Accessing an instance by using the API"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/accessing-by-API"
---

Elasticsearch provides a full\-featured RESTful API to interact with instances. Cloud Search provides a Virtual Private Cloud (VPC) endpoint for each instance. You can access the instance from an Elastic Compute Service (ECS) instance that resides in the same VPC as the instance. This topic describes how to use the API to access an ES instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Before you access an instance, confirm whether the port corresponding to the security group is enabled.

<span id=".5p-l55yL6K6_6Zeu5Zyw5Z2A"></span>
## Viewing the endpoint


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. On the **List of Instances** page, click the name of the target instance.

3. On the **Instance information** page, click **Service access** to get the endpoint of the instance.


<span id=".5rWL6K-V6K6_6Zeu"></span>
## Testing connectivity

You can run a `curl` command to test whether your instance can be accessed normally. The `ping` command is not supported for connectivity testing.


* For instances for which the ES user logon authentication is enabled, username and password authentication is required for logons. The specific command is as follows:

   ```SQL
   curl action -u user:password host
   ```
   

   * user: the username for logging on to the instance.

   * password: the password for logging on to the instance.

   * host: the private or public endpoint of the instance. You can get this endpoint on the **Instance information** page.

* If you want to quickly access and test the instance for which HTTPS is enabled, add the `--insecure` parameter to the `curl` command.


In this topic, the private endpoint is used in the example to illustrate how to access the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following commands are run on an ES instance with version <code>7.10.2</code> because some commands are not supported in earlier versions.</div>


Run the following command:

```SQL
# ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
curl -XGET  -u user:password http://192.168.*.*:9200
```


If information similar to the following is returned, the instance can be accessed normally. The return values vary based on the instance version.

```SQL
{
  "name" : "es-master-wq83vr6wv6w0****-2",
  "cluster_name" : "wq83vr6wv6w0d1hu",
  "cluster_uuid" : "97uFBD01TZuA_pyDT6****",
  "version" : {
    "number" : "7.10.2",
    "build_flavor" : "oss",
    "build_type" : "tar",
    "build_hash" : "2f32220",
    "build_date" : "2019-04-02T15:59:27.961366Z",
    "build_snapshot" : false,
    "lucene_version" : "8.7.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```


<span id=".5Yib5bu65paH5qGj"></span>
## Creating documents

<span id=".5Yib5bu65Y2V5Liq5paH5qGj"></span>
### Creating a single document

Run the following command to create an index named `customer` and add a document whose `id` is 1 to the index.

```SQL
# ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
curl -XPUT -u admin:P_ssw0rd http://192.168.*.*:9200/customer/_doc/1 -H 'Content-Type: application/json' -d '
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

```SQL
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


<span id=".5Yib5bu65aSa5Liq5paH5qGj"></span>
### Creating multiple documents

Run the following command to add multiple documents to an index at a time.

```SQL
# ES user logon authentication is enabled by default. Make sure that you enter the correct username and password.
curl -XPOST -u admin:P_ssw0rd http://192.168.*.*:9200/_bulk -H 'Content-Type: application/json' -d '
{"index" : { "_index": "customer","_id":2} }
{"name":"Tom","address":"Haidian District","city":"Beijing","age":"23","birthday":"1998-01-01","level":{"viplevel":3,"viptype":"Premium VIP"}}
{"index" : { "_index": "customer","_id":3} }
{"name":"Joe","address":"Binjiang District, Hangzhou City, Zhejiang Province","city":"Hangzhou","age":"30","birthday":"1991-05-05","level":{"viplevel":5,"viptype":"Diamond VIP"}}
'
```


The following information is returned:

```SQL
{"took":15,"errors":false,"items":[{"index":{"_index":"customer","_type":"_doc","_id":"2","_version":2,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":6,"_primary_term":1,"status":200}},{"index":{"_index":"customer","_type":"_doc","_id":"3","_version":2,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":7,"_primary_term":1,"status":200}}]}
```


<span id=".5pu05paw5paH5qGj"></span>
## Updating documents

Rerun the command for creating a single document to update the document that corresponds to a specified ID.

After the document is updated, information similar to the following is returned:

```SQL
{
"_index":"customer",
"_type":"_doc",
"_id":"1",
"_version":1,
"result":"updated",
"_shards":{
    "total":2,
    "successful":1,
    "failed":0
},
"_seq_no":9,
"_primary_term":1
}
```


<span id=".5p-l6K-i5paH5qGj"></span>
## Querying documents

<span id=".5p-l6K-i5oyH5a6aIElE"></span>
### Querying a document with a specified ID

```SQL
curl -XGET -u admin:P_ssw0rd  'http://192.168.*.*:9200/customer/_doc/1?pretty' -H 'Content-Type: application/json'
```


The following information is returned:

```SQL
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


<span id=".5p-l6K-i5p-Q5Liq57Si5byV"></span>
### Querying and indexing all documents

```SQL
curl -XGET -u admin:P_ssw0rd  'https://192.168.*.*:9200/customer/_doc/_search?pretty' -H 'Content-Type: application/json' 
```


The following information is returned:

```SQL
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


<span id=".5aSN5p2C5p-l6K-i"></span>
### Implementing complex queries

You can build commands to implement more complex queries.

For example, to achieve the same query result as the SQL statement `select * from customer where level.viplevel=5`, you can build the following command:

```SQL
curl -XGET -u admin:P_ssw0rd  'https://192.168.*.*:9200/customer/_doc/_search?pretty' -H 'Content-Type: application/json' -d '
{
  "query" : {
      "constant_score" : { 
          "filter" : {
              "term" : { 
                  "level.viplevel" : 5
              }
          }
      }
  }
}'
```


The following information is returned:

```SQL
{
  "took" : 4,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
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
      }
    ]
  }
}
```


<span id=".6IGa5ZCI5p-l6K-i"></span>
### Implementing aggregation queries

You can build commands to implement complex aggregation queries.

For example, to achieve the same query result as the SQL statement `select level.viplevel, count(1) from customer group by level.viplevel`, you can build the following command:

```SQL
curl -XGET -u admin:P_ssw0rd  'https://192.168.*.*:9200/customer/_doc/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "size" : 0,
  "aggs" : { 
      "vip_level" : { 
          "terms" : { 
            "field" : "level.viplevel"
          }
      }
  }
}'
```


The following information is returned:

```SQL
{
  "took" : 3,
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
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "vip_level" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : 3,
          "doc_count" : 2
        },
        {
          "key" : 5,
          "doc_count" : 1
        }
      ]
    }
  }
}
```


<span id=".5Yig6Zmk5paH5qGj"></span>
## Deleting documents

<span id=".5Yig6Zmk5Y2V5Liq5paH5qGj"></span>
### Deleting a single document

```SQL
curl -XDELETE -u admin:P_ssw0rd  'https://192.168.*.*:9200/customer/_doc/1?pretty' -H 'Content-Type: application/json' 
```


The following information is returned:

```SQL
{
  "_index" : "customer",
  "_type" : "_doc",
  "_id" : "1",
  "_version" : 7,
  "result" : "deleted",
  "_shards" : {
    "total" : 2,
    "successful" : 2,
    "failed" : 0
  },
  "_seq_no" : 10,
  "_primary_term" : 1
}
```


<span id=".5Yig6Zmk57Si5byV"></span>
### Deleting an index

```SQL
curl -XDELETE -u admin:P_ssw0rd 'https://192.168.*.*:9200/customer?pretty' -H 'Content-Type: application/json' 
```


The following information is returned:

```SQL
{
    "acknowledged" : true
}
```
