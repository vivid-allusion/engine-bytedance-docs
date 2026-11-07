---
title: "Access an HBase instance from a Python program using a Thrift2 address"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Access_an_HBase_instance_from_a_Python_program_using_a_Thrift2_address"
---

By default, Table Storage for HBase provides a ZK connection address for accessing instances and supports Thrift connections to meet multi\-language development needs. Thrift is a built\-in service component in standard HBase instances. Developed on the Apache Thrift communication framework, it allows access from multiple programming languages. This article describes the steps to access an HBase instance from a Python program via a Thrift2 address.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* To access the HBase instance over the private network, you must meet the following requirements:

   * The purchased ECS server and the HBase instance are in the same Virtual Private Cloud (VPC). For instructions on how to purchase an ECS server, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * The IP address of the ECS server has been added to the HBase allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* To access the HBase instance over the public network, ensure that the IP address of the device running the Python tool is added to the instance's allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* Python is installed on your ECS instance or local device. Python 3.x.x is recommended. You can run the `python version` command to check your current Python version.

* You must have the Thrift service installed on your ECS instance or local device. We recommend using version 0.14.2 or later. For more information about the Thrift service, see [Apache Thrift](https://thrift.apache.org/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Get the high\-availability Thrift connection address of the HBase instance.

   To view the connection address, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the high\-availability Thrift connection address is not enabled for Table Storage for HBase. To enable it, see <a href="https://docs.byteplus.com/en/docs/HBase/Enabling_or_disabling_high-availability_Thrift_connection_address">Enable high\-availability Thrift connection address</a>.   </div>
   

2. Download and install the HBase Thrift module.

   1. Download the compiled [Thrift file](https://db-tw-only-no-delete.tos-cn-beijing.volces.com/Hbase%E6%96%87%E6%A1%A3%E4%B8%AD%E9%9C%80%E8%A6%81%E4%B8%8B%E8%BD%BD%E7%9A%84%E7%9B%B8%E5%85%B3%E6%96%87%E4%BB%B6/gen-py.tar.gz), which contains the HBase Thrift module for Python access, and save it to the ECS instance or local device where the Thrift service is installed.

      ```bash
      # Unzip the downloaded Thrift file
      tar -zxvf gen-py.tar.gz
      # Enter the gen-py directory
      cd gen-py
      ```
      

   2. Configure the Python environment variables to reference the HBase Thrift module. Move the `hbase` files in the `gen-py` directory to the Python installation directory.

      The command is as follows.

      ```bash
      mv hbase/ /<ECS 实例或本地设备上 Python 的安装目录>/Python/3.8/lib/python/site-packages/
      ```
      

   3. Install the HBase Thrift module.

      The command is as follows.

      ```bash
      pip install thrift
      ```
      

3. Access the HBase instance from a Python program using the Thrift2 address.

   The code is as follows.

   ```python
   # encoding:utf-8
   # !/usr/bin/env python3
   
   import random
   
   # Open a Thrift2 connection using TTransport, TSocket, and TBinaryProtocol.
   from thrift.transport import TTransport
   from thrift.transport import TSocket
   from thrift.protocol import TBinaryProtocol
   
   # From thrift --gen py hbase.thrift
   from hbase import THBaseService
   from hbase.ttypes import TPut, TColumnValue, TGet, TNamespaceDescriptor, TTableDescriptor, TColumnFamilyDescriptor, \
       TTableName, TScan
   
   
   class Demo:
       def __init__(self, host, port):
           socket = TSocket.TSocket(host=host, port=port)
           self.transport = TTransport.TFramedTransport(socket)
           protocol = TBinaryProtocol.TBinaryProtocol(self.transport)
   
           self.client = THBaseService.Client(protocol)
           self.transport.open()
   
       def __del__(self):
           self.transport.close()
   
       def get_ns_list(self):
           return [ns.name for ns in self.client.listNamespaceDescriptors()]
   
       def namespace_exists(self, namespace):
           return namespace in self.get_ns_list()
   
       def create_ns(self, namespace):
           if not self.namespace_exists(namespace):
               self.client.createNamespace(TNamespaceDescriptor(name=namespace))
   
       def create_table(self, table_name, column_family, namespace="ns"):
           if not self.namespace_exists(namespace):
               self.client.createNamespace(TNamespaceDescriptor(name=namespace))
           if not self.table_exists(namespace, table_name):
               _table_name = TTableName(
                   ns=namespace.encode("utf8"), qualifier=table_name.encode("utf8")
               )
               self.client.createTable(
                   TTableDescriptor(
                       tableName=_table_name,
                       columns=[
                           TColumnFamilyDescriptor(name=column_family.encode("utf8"))
                       ],
                   ),
                   None,
               )
   
       def table_exists(self, namespace, table_name):
           namespace = namespace.encode("utf8")
           table_name = table_name.encode("utf8")
           _table_name = TTableName(ns=namespace, qualifier=table_name)
           return self.client.tableExists(_table_name)
   
       def put(self, namespace, table_name, row_key, family, qualifier, value):
           row_key, family = row_key.encode("utf8"), family.encode("utf8")
           qualifier, value = qualifier.encode("utf8"), value.encode("utf8")
           table_in_bytes = self._table_in_bytes(namespace, table_name)
           put = TPut(
               row=row_key,
               columnValues=[
                   TColumnValue(family=family, qualifier=qualifier, value=value)
               ],
           )
           self.client.put(table_in_bytes, put)
   
       def get(self, namespace, table_name, row_key):
           row_key = row_key.encode("utf8")
           table_in_bytes = self._table_in_bytes(namespace, table_name)
           get = TGet(row=row_key)
           result = self.client.get(table_in_bytes, get)
           return result
   
       def scan(self, namespace, table_name, start_row, stop_row):
           start_row, stop_row = start_row.encode("utf8"), stop_row.encode("utf8")
           table_in_bytes = self._table_in_bytes(namespace, table_name)
           scan = TScan(startRow=start_row, stopRow=stop_row)
           caching = 2
           results = []
           while True:
               last_result = None
               current_results = self.client.getScannerResults(
                   table_in_bytes, scan, caching
               )
               for result in current_results:
                   results.append(result)
                   last_result = result
               if last_result is None:
                   break
               else:
                   next_start_row = self._create_closest_row_after(last_result.row)
                   scan = TScan(startRow=next_start_row, stopRow=stop_row)
           return results
   
       def batch_put(self, namespace, table_name):
           """
           puts = [TPut(row="row2".encode("utf8"), columnValues=[TColumnValue(family="f".encode("utf8"),
           qualifier="q1".encode("utf8"), value="value2".encode("utf8"))]), ...]
           """
           puts = [TPut(row="row1".encode("utf8"), columnValues=[TColumnValue(family="cf1".encode("utf8"),
                                                                              qualifier="q1".encode("utf8"),
                                                                              value="value1".encode("utf8"))]),
                   TPut(row="row2".encode("utf8"), columnValues=[TColumnValue(family="cf1".encode("utf8"),
                                                                              qualifier="q2".encode("utf8"),
                                                                              value="value2".encode("utf8"))])]
           table_in_bytes = self._table_in_bytes(namespace, table_name)
           self.client.putMultiple(table=table_in_bytes, tputs=puts)
   
       def batch_get(self, namespace, table_name):
           """
           gets = [TGet(row="row2".encode("utf8")), ...]
           """
           gets = [TGet(row="row1".encode("utf8")), TGet(row="row2".encode("utf8"))]
           table_in_bytes = self._table_in_bytes(namespace, table_name)
           self.client.getMultiple(table_in_bytes, gets)
   
       def get_table_descriptor(self, ns, table):
           """
           res struct:
           {
               "cf1": {"attr1": value1, "attr2": value2, ....},
               "cf2": {"attr1": value1, "attr2": value2, ....},
               .....
           }
           """
           table = table.encode("utf8")
           ns = ns.encode("utf8")
           table = TTableName(ns=ns, qualifier=table)
           info = self.client.getTableDescriptor(table)
           res = {}
           if info and info.columns:
               for item in info.columns:
                   attributes = item.attributes
                   new_attr = {}
                   for key, value in attributes.items():
                       new_attr[self._bytes_to_str(key)] = self._bytes_to_str(value)
                   res[self._bytes_to_str(item.name)] = new_attr
   
           table_attr = {}
           for key, value in info.attributes.items():
               table_attr[self._bytes_to_str(key)] = self._bytes_to_str(value)
   
           return table_attr, res
   
       def delete(self, namespace, table):
           namespace, table = namespace.encode("utf8"), table.encode("utf8")
           # disable
           self.client.disableTable(TTableName(ns=namespace, qualifier=table))
           # drop
           self.client.deleteTable(TTableName(ns=namespace, qualifier=table))
   
       @staticmethod
       def _bytes_to_str(byte_str):
           return bytes.decode(byte_str)
   
       @staticmethod
       def _table_in_bytes(namespace, table_name):
           return "{namespace}:{table_name}".format(
               namespace=namespace, table_name=table_name
           ).encode("utf8")
   
       @staticmethod
       def _create_closest_row_after(row):
           array = bytearray(row)
           array.append(0x00)
           return bytes(array)
   
   
   def unit_test():
       client = Demo(host="xxx", port=9090)
       name_space = "ns6"
       table = "table6"
       column = "cf1"
       client.create_table(table, column, name_space)
       print(client.table_exists(name_space, table))
       for i in range(10):
           row_key = "row" + str(i)
           client.put(name_space, table, row_key, column, "name", "handsome_boy" + str(i))
       # client.batch_put(name_space, table)
       # scan
       start_row = "row0"
       stop_row = "row8"
       result = client.scan(name_space, table, start_row, stop_row)
       print(result)
       result = client.get(name_space, table, "row4")
       # client.batch_get(name_space, table)
       # result = client.get_table_descriptor(name_space, table)
       # client.delete(name_space, table)
       # result = client.table_exists(name_space, table)
       print(result)
   
   
   if __name__ == "__main__":
       unit_test()
       
   ```
