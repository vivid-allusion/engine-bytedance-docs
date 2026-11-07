---
title: "User guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/livy_User_guide"
---

<span id="_1-livy-介绍"></span>
## 1 Introduction to Livy

[Apache Livy](https://livy.apache.org/) is a REST service that allows users to Submit Job to a Spark cluster through a REST API. Its architecture is as follows

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5469ece5f505682e494b9d4774442ce4.png) </span>

Users Submit Job requests to the Livy server via the REST API, after which the server submits Spark jobs to the cluster manager (typically YARN). Spark jobs run in cluster mode, meaning the Spark context runs within the cluster rather than on the Livy server. Livy then manages these Spark jobs using sessions.

<span id="_2-livy-入门"></span>
## 2 Getting started with Livy

<span id="_2-1-rest-api"></span>
### 2.1 Rest API

Session is a very important concept in Livy, and almost all operations revolve around it.

The following is an example:

```python
import json, pprint, requests, textwrap

# 1. Open a session
host = 'http://localhost:8899'
data = {'kind': 'spark'}
headers = {'Content-Type': 'application/json'}
r = requests.post(host + '/sessions', data=json.dumps(data), headers=headers)
r.json()

{u'state': u'starting', u'id': 0, u'kind': u'spark'}

# 2. Query the session status. The newly created session is in the idle state.
session_url = host + r.headers['location']
r = requests.get(session_url, headers=headers)
r.json()

{u'state': u'idle', u'id': 0, u'kind': u'spark'}

# 3. Send a piece of code, which is the Spark code for calculating Pi. At this point, the session is in the running state, and the Spark job on the cluster is also running.
data = {
  'code': textwrap.dedent("""
    val NUM_SAMPLES = 100000;
    val count = sc.parallelize(1 to NUM_SAMPLES).map { i =>
      val x = Math.random();
      val y = Math.random();
      if (x*x + y*y < 1) 1 else 0
    }.reduce(_ + _);
    println(\"Pi is roughly \" + 4.0 * count / NUM_SAMPLES)
    """)
}
r = requests.post(statements_url, data=json.dumps(data), headers=headers)
pprint.pprint(r.json())

# 4. Retrieve the calculation result
statement_url = host + r.headers['location']
r = requests.get(statement_url, headers=headers)
pprint.pprint(r.json())

{u'id': 1,
 u'output': {u'data': {u'text/plain': u'Pi is roughly 3.14004\nNUM_SAMPLES: Int = 100000\ncount: Int = 78501'},
             u'execution_count': 1,
             u'status': u'ok'},
 u'state': u'available'}
 
 # 5. Close the session, and the Spark context will exit accordingly
session_url = 'http://localhost:8998/sessions/0'
requests.delete(session_url, headers=headers)
```


The above job submission is a piece of Scala code. Users can also Submit Job for PySpark, SparkR, and many other types. Different job types are identified by the `kind` field when submitting jobs. Supported `kind` values are:


* spark

* pyspark

* sparkr

* sql


In addition to the `kind` field, a session has other fields, such as session status, specifying jars when submitting jobs, Spark job parameters, and so on. For more details, refer to the [official documentation](https://livy.incubator.apache.org/examples/).

<span id="_2-2-java-api"></span>
### 2.2 Java API

Livy also provides a Java client encapsulated based on the REST API. The following is an example for Spark 3.2.1 and later versions.


1. First, import Livy's jar:

   ```python
   <dependency>
     <groupId>org.apache.livy</groupId>
     <artifactId>livy-client-http</artifactId>
     <version>0.8.0-incubating</version>
   </dependency>
   ```
   

2. When using Livy, users need to implement the Job abstraction defined by Livy beforehand. The following is an example for calculating Pi:

   ```java
   import java.util.*;
   
   import org.apache.spark.api.java.*;
   import org.apache.spark.api.java.function.*;
   
   import org.apache.livy.*;
   
   public class PiJob implements Job<Double>, Function<Integer, Integer>,
     Function2<Integer, Integer, Integer> {
   
     private final int samples;
   
     public PiJob(int samples) {
       this.samples = samples;
     }
   
     @Override
     public Double call(JobContext ctx) throws Exception {
       List<Integer> sampleList = new ArrayList<Integer>();
       for (int i = 0; i < samples; i++) {
         sampleList.add(i + 1);
       }
   
       return 4.0d * ctx.sc().parallelize(sampleList).map(this).reduce(this) / samples;
     }
   
     @Override
     public Integer call(Integer v1) {
       double x = Math.random();
       double y = Math.random();
       return (x*x + y*y < 1) ? 1 : 0;
     }
   
     @Override
     public Integer call(Integer v1, Integer v2) {
       return v1 + v2;
     }
   }
   ```
   

3. Then submit this job using Livy's API:

   ```java
   LivyClient client = new LivyClientBuilder()
     .setURI(new URI(livyUrl))
     .build();
   
   try {
     System.err.printf("Uploading %s to the Spark context...\n", piJar);
     client.uploadJar(new File(piJar)).get();
   
     System.err.printf("Running PiJob with %d samples...\n", samples);
     double pi = client.submit(new PiJob(samples)).get();
   
     System.out.println("Pi is roughly: " + pi);
   } finally {
     client.stop(true);
   }
   ```
   


<span id="_3-重要参数"></span>
## 3 Important parameters

There are several important parameters in Livy. Not understanding them may lead to unexpected behavior.


|Configuration name |Default value |Description |
|---|---|---|
|livy.server.host |0.0.0.0 |The IP address to which the Livy server binds. The default value binds to all network interfaces. |
|livy.server.port |8998 |The port to which the Livy server binds |
|livy.spark.master |local |The Spark \-\-master parameter. For YARN environments, it is recommended to set this to yarn. |
|livy.spark.deploy\-mode | |The Spark \-\-deploy\-mode parameter. For YARN environments, it is recommended to set this to cluster. |
|livy.server.session.timeout\-check |true |Whether to perform expiration checks on sessions. It is recommended to enable this. |
|livy.server.session.timeout\-check.skip\-busy |false |Whether to skip checks for busy sessions (that is, sessions with running tasks). The default value is false. It is recommended to set it to true; otherwise, running jobs may be killed due to timeout. |
|livy.server.session.timeout |1h |Session timeout duration. If set too short, session timeouts may occur frequently. If the parameter is set too high, there may be many idle sessions, resulting in wasted cluster resources. |
|livy.cache\-log.size |200 |Cached log size, Unit: MB |


In addition, Livy has several other important parameters, including


* Access control

* Yarn app leakage check

* State recovery


and more. Refer to Livy's conf [template](https://github.com/apache/incubator-livy/blob/master/conf/livy.conf.template).
