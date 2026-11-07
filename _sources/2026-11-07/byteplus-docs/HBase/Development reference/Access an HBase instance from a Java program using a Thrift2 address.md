---
title: "Access an HBase instance from a Java program using a Thrift2 address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Java_program_using_a_Thrift2_address"
---

By default, Table Storage for HBase provides a ZK connection address for accessing instances and supports Thrift connections to meet multi\-language development needs. Thrift is a built\-in service component in standard HBase instances. Developed on the Apache Thrift communication framework, it allows access from multiple programming languages. This article describes the steps to access an HBase instance from a Java program using a Thrift2 address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* To access the HBase instance over the private network, you must meet the following requirements:

   * The purchased ECS server and the HBase instance are in the same Virtual Private Cloud (VPC). For instructions on how to purchase an ECS server, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * The IP address of the ECS server has been added to the HBase allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* To access the HBase instance over the public network, ensure that the IP address of the device running the Java tool is added to the instance's allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* A Java environment is installed on the ECS instance or your local device. We recommend using JDK 8. For more details, see [Java Downloads](https://www.oracle.com/java/technologies/downloads/#java8).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Get the high\-availability Thrift connection address of the HBase instance.

   To view the connection address, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the high\-availability Thrift connection address is not enabled for Table Storage for HBase. To enable it, see <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address">Enable high\-availability Thrift connection address</a>.   </div>
   

2. Configure the high\-availability Thrift connection address to access the HBase instance.

   Set the following configurations in your business code to connect to the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${HBase high-availability Thrift connection address}, ${port number}</code> in your code with the Thrift2 connection address and port number of your HBase instance. You can then use the following sample code to access the HBase instance. The following code provides examples for defining a table, writing data, and reading data.   </div>
   

   ```java
   package com.bytedance.hbase.example;
   
   import org.apache.hadoop.hbase.thrift2.generated.TColumn;
   import org.apache.hadoop.hbase.thrift2.generated.TColumnValue;
   import org.apache.hadoop.hbase.thrift2.generated.TGet;
   import org.apache.hadoop.hbase.thrift2.generated.THBaseService;
   import org.apache.hadoop.hbase.thrift2.generated.TPut;
   import org.apache.hadoop.hbase.thrift2.generated.TResult;
   import org.apache.hadoop.hbase.thrift2.generated.TScan;
   import org.apache.thrift.protocol.TBinaryProtocol;
   import org.apache.thrift.protocol.TProtocol;
   import org.apache.thrift.transport.TSocket;
   import org.apache.thrift.transport.TTransport;
   import org.apache.thrift.transport.layered.TFramedTransport;
   
   import java.nio.ByteBuffer;
   import java.util.Arrays;
   import java.util.List;
   
   public class HBaseThriftExample {
   
     public static void main(String args[]) throws Exception{
       // Open a Thrift2 connection to an HBase instance via TSocket and TBinaryProtocol
       TSocket socket = new TSocket("${HBase高可用Thrift连接地址}", ${端口号});
       TTransport transport = new TFramedTransport(socket);
       TProtocol protocol = new TBinaryProtocol(transport);
   
       THBaseService.Iface client = new THBaseService.Client(protocol);
       transport.open();
   
       //Define table information
       ByteBuffer table = ByteBuffer.wrap(${"table name"}.getBytes());
       ByteBuffer row = ByteBuffer.wrap(${"row name"}.getBytes());
       ByteBuffer family = ByteBuffer.wrap(${"columnfamily name"}.getBytes());
       ByteBuffer qualifier = ByteBuffer.wrap(${"qualifier name"}.getBytes());
       ByteBuffer value = ByteBuffer.wrap(${"column value"}.getBytes());
   
       // Update existing data or insert new data through TPut
       System.out.println("---put or update a key---");
       TPut put = new TPut();
       put.setRow(row);
       TColumnValue colVal = new TColumnValue(family, qualifier, value);
       put.setColumnValues(Arrays.asList(colVal));
       client.put(table, put);
   
       // Query information about specified or all columns and column families through TGet
       System.out.println("---get a row---");
       TGet get = new TGet();
       get.setRow(row);
       TColumn col = new TColumn()
               .setFamily(family)  // Do not specify a column family, that is, get all column families
               .setQualifier(qualifier); // Do not specify a column name, that is, get all columns
       get.setColumns(Arrays.asList(col));
       TResult result = client.get(table, get);
       //System.out.println("get row : " + new String(result.getRow()));
   
       result.getColumnValues().forEach(c -> {
         System.out.println(new String(result.getRow()) + "  " + new String(c.getFamily()) + "_" +
                 new String(c.getQualifier()) + ":" + new String(c.getValue()));
       });
   
       // Query the information of the entire table through TScan
       System.out.println("---scan a table---");
       TScan scan = new TScan();
       List<TResult> resultList = client.getScannerResults(table, scan, 2);
       resultList.forEach(r -> r.getColumnValues().forEach(c -> {
         System.out.println(new String(r.getRow()) + "  " + new String(c.getFamily()) + "_" +
                 new String(c.getQualifier()) + ":" + new String(c.getValue()));
       }));
   
       // Close the Thrift2 connection via the close function
       transport.close();
       socket.close();
     }
   
   }
   ```
   


<span id=".55u45YWz5pON5L2c"></span>
## Related operations

You can also download the [HBase Java code project demo](https://tobsre.tos-cn-shanghai.volces.com/hbase-thrift-java.tar.gz) and replace variables such as the Thrift2 connection address and table name before use.
