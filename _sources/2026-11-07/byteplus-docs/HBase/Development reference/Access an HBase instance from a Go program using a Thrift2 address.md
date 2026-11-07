---
title: "Access an HBase instance from a Go program using a Thrift2 address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Go_program_via_a_Thrift2_address"
---

By default, Table Storage for HBase provides a ZK connection address for accessing instances and supports Thrift connections to meet multi\-language development needs. Thrift is a built\-in service component in standard HBase instances. Developed on the Apache Thrift communication framework, it allows access from multiple programming languages. This article describes the steps to access an HBase instance from a Go program via a Thrift2 address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* To access the HBase instance over the private network, you must meet the following requirements:

   * The purchased ECS server and the HBase instance are in the same Virtual Private Cloud (VPC). For instructions on how to purchase an ECS server, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * The IP address of the ECS server has been added to the HBase allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* To access the HBase instance over the public network, ensure the IP address of the device running the Go program is added to the HBase instance's allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* You must have a Go program installed on your ECS instance or local device. We recommend using Go 1.20.x or a later version. You can run the `go version` command to check the current version of Go.

* You must have the Thrift service installed on your ECS instance or local device. We recommend using version 0.14.2 or later. For more information about the Thrift service, see [Apache Thrift](https://thrift.apache.org/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Get the high\-availability Thrift connection address of the HBase instance.

   To view the connection address, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the high\-availability Thrift connection address is not enabled for Table Storage for HBase. To enable it, see <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address">Enable high\-availability Thrift connection address</a>.   </div>
   

2. Download and decompress the [Go Thrift2](https://db-tw-only-no-delete.tos-cn-beijing.volces.com/Hbase%E6%96%87%E6%A1%A3%E4%B8%AD%E9%9C%80%E8%A6%81%E4%B8%8B%E8%BD%BD%E7%9A%84%E7%9B%B8%E5%85%B3%E6%96%87%E4%BB%B6/hbasegothrift2.tar.gz) file on your ECS instance or local device to connect your Go program to an HBase instance by using Thrift2.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to numerous compatibility issues, compiling the HBase Thrift2 file yourself is not recommended. We suggest you download and use the provided file directly.   </div>
   

   ```bash
   # Decompress the downloaded file
   tar -zxvf hbasegothrift2.tar.gz
   # Go to the hbase directory
   cd hbase
   ```
   

3. Replace `<YourPublicThriftIP>` in the `main.go` file with the actual Thrift2 connection address, then compile and run it.

   ```bash
   # Edit the main.go file.
   vim main.go
   # Compile the *.go files.
   go build *.go
   # Run the relevant code.
   ./hbase
   ```
   

4. The sample code is as follows.

   ```go
   package main
   
   import (
      "context"
      "fmt"
      "github.com/apache/thrift/lib/go/thrift"
      "net"
      "os"
   )
   
   func main() {
   // Replace <YourPublicThriftIP> with the actual Thrift2 connection address
      host := "<YourPublicThriftIP>"
      port := "9090"
   
      protocolFactory := thrift.NewTBinaryProtocolFactoryDefault()
      socket, err := thrift.NewTSocket(net.JoinHostPort(host, port)) // Create a persistent connection
      if err != nil {
         fmt.Println("failed to create new socket err: " + err.Error())
         os.Exit(1)
      }
      transport := thrift.NewTFramedTransport(socket) // Wrap a TFramedTransport
   
      // The client is associated with a connection and is not thread-safe.
      client := NewTHBaseServiceClientFactory(transport, protocolFactory) // Associate the HBase client with the connection.
      // Perform the connection operation.
      if err := transport.Open(); err != nil {
         fmt.Fprintln(os.Stderr, "Error opening socket to "+host+":"+port, " ", err)
         os.Exit(1)
      }
      defer transport.Close() // Close the connection when finished.
   
      ctx := context.Background()
   
      tableName := "demo_test_table"
      columnFamily := []byte("cf")
      // Data expiration time, for example, 7 days.
      var ttl int32 = 7 * 86400
      columnFamilies := []*TColumnFamilyDescriptor{
         {
            Name:       columnFamily,
            TimeToLive: &ttl,
            // FAST_DIFF
            DataBlockEncoding: TDataBlockEncodingPtr(TDataBlockEncoding_FAST_DIFF),
            // lz4 compression
            CompressionType: TCompressionAlgorithmPtr(TCompressionAlgorithm_LZ4),
         },
      }
      descriptor := &TTableDescriptor{
         TableName: &TTableName{
            Qualifier: []byte(tableName),
         },
         Columns: columnFamilies,
      }
      exists, err := client.TableExists(ctx, descriptor.TableName)
      if err != nil {
         fmt.Println("table exist err :" + err.Error())
         return
      }
      if !exists {
         err = client.CreateTable(ctx, descriptor, nil)
         if err != nil {
            fmt.Println("create table err :" + err.Error())
            return
         }
      }
   
      put := &TPut{
         Row: []byte("foo-row"),
         ColumnValues: []*TColumnValue{
            {
               Family:    columnFamily,
               Qualifier: []byte("sample"),
               Value:     []byte("bar"),
            },
         },
      }
      err = client.Put(ctx, []byte(tableName), put)
      if err != nil {
         fmt.Println("create table err :" + err.Error())
         return
      }
   
      get := &TGet{
         Row: []byte("foo-row"),
      }
      result, err := client.Get(ctx, []byte(tableName), get)
      if err != nil {
         fmt.Println("get err :" + err.Error())
         return
      }
      if result != nil {
         fmt.Println("get ret success")
         fmt.Println("Rowkey:" + string(result.GetRow()))
         for _, cv := range result.ColumnValues {
            fmt.Println("Family:", string(cv.Family), "Qualifer:", string(cv.Qualifier), "Value:", string(cv.Value))
         }
      } else {
         fmt.Println("get ret is nil")
      }
   
   }
   ```
