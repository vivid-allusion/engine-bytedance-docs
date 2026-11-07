---
title: "Manage UDF"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-udf"
---

ByteHouse supports creating user\-defined functions (User\-Defined Function, UDF) to meet the needs of user\-defined computational logic in business scenarios. This article introduces how to create, edit, and delete UDFs.

<span id="4347e2c4"></span>
# Usage restrictions

Only users with the SystemAdmin role can create and manage UDF permissions.

<span id="3e553923"></span>
# Function overview

UDFs (User\-Defined Functions) are custom functions created by users, typically used in database systems or programming environments to meet specific computational requirements. You can extend built\-in functions by writing custom logic in specific programming languages like SQL, Python, or Java to achieve more complex or personalized data processing.

Currently, ByteHouse supports executable user\-defined functions (Executable UDF), which run native scripts when calling the UDF. The current version supports Python scripts.

<span id="b2f71f97"></span>
# Create UDF


1. Log in to the ByteHouse enterprise console, click **Data Manage** at the top, select the successfully created cluster from the dropdown in the upper left corner, click the ➕ **New** button, and choose **Create UDF**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0375e03421ed4a2da430f885b080123a~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the UDF basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4f669e798b54f6e93bc5fcbf202efaf~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration description |
   |---|---|
   |Cluster |Select an existing cluster; subsequent UDFs will be created in this cluster. |
   |UDF type |Currently, only the Executable type is supported. |
   |Name |Custom UDF name. Naming rules are as follows:<br><br><br>* Cannot start with a number<br><br>* Cannot contain spaces<br><br>* Can only contain letters, numbers, and underscores |
   |description |Customize UDF description information.<br><br>All users can see the UDF description; it is recommended to include examples in the description box to assist users in using the UDF in SQL worksheets |
   

3. Fill in the UDF configuration information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92cd28e946f247a98b5c0c6c58917d97~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Input value |Configure the input parameter names and types for the UDF. To add multiple params, click the + button to continue adding.<br><br>Param names must start with a letter or underscore and can include letters, numbers, and underscores. |
   |Result value |Configure the output param name and param type of the UDF.<br><br>Param names must start with a letter or underscore and can include letters, numbers, and underscores. |
   |Format |Currently, only TabSeparated format is supported. |
   |Upload file(s) |Upload the UDF script file. Currently, only .py format is supported, with a single file size not exceeding 10M.<br><br>You can click **Python Template Download** to download the template and customize function information as needed according to the template description below. |
   

   Python template content and description are as follows:

   ```Python
   # When format is TabSeperated, input parameters are separated by tabs in the standard input stream
   # Each line represents a set of input parameters, and the corresponding output line needs to be produced in the standard output stream
   def concat_three_elem():
       import sys
       for line in sys.stdin:
           # Remove the newline character at the end of the line and split by tabs
           parts = line.strip().split('    ')
           # Ensure there are three parameters
           if len(parts) == 3:
               # Concatenate the three parameters
               output = ''.join(parts)
               print(output)
           else:
               print("Each row should contain three parameters separated by Tab")
   if __name__ == "__main__":
       concat_three_elem()
   ```
   

   
   |Code |Description |
   |---|---|
   |for line in sys.stdin |Processes data line by line. sys.stdin is the standard input stream, corresponding to the input value. |
   |parts = line.strip().split(' ') |Removes the newline character at the end of each line and splits the string by Tab key to divide one line of input into multiple params. |
   |if len(parts) == 3 |Verifies whether the number of entered params equals 3. |
   |output = ''.join(parts) |The output is the concatenation of the params list as a string. |
   |print(output) |Automatically captured as the return value; print only once per line, or it will cause an error. |
   

4. Click **Create** immediately. The system prompts **Creation successful** and redirects to the UDF detail page.

5. Restart the cluster. After creating the UDF, restart the cluster to activate it. For operation details, please refer to [Restart a cluster](https://docs.byteplus.com/docs/bytehouse/restart-a-cluster).


<span id="bc4b0fcc"></span>
# Edit UDF

ByteHouse supports editing created UDFs


1. Log in to the ByteHouse Enterprise Console, click **Data Management** at the top, select the successfully created cluster from the top\-left dropdown, click the UDF folder in the list, then click the **target UDF name**

2. On the UDF detail page, click **Edit**.

3. On the edit UDF page, modify the description and configuration information as needed

4. Click **Save**.


<span id="0564ec4e"></span>
# Delete UDF


1. Log in to the ByteHouse Enterprise Console, click **Data Management** at the top, select the successfully created cluster from the top\-left dropdown, click the UDF folder in the list, then click the **target UDF name**

2. On the UDF detail page, click  **...**  button, then click **Delete**.


<span id="82d57856"></span>
# Related reference: Grant users UDF permissions

You can refer to the following documents to grant users the related UDF permissions:


* [Role management](https://docs.byteplus.com/docs/bytehouse/role-management)

* [IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management)
