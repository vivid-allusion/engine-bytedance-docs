---
title: "FTP Data Connection"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/FTP_Data_Connection"
---

Users can set up their own FTP server, and regularly push data into the FTP server in the form of files. The system supports downloading data by connecting to the FTP server, and then structurally mapping files into related table structures for the system to identify and read to achieve data connection. This article explains how to access FTP data.

<span id="f50960b0"></span>
# Conditions of use

Users need to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to use this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="5bc005dc"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **Web Connector \- FTP/SFTP** data connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a6ee1783164a8f8f077cc70c26e84a~tplv-goo7wpa0wc-image.image) </span>


3. On the edit page, configure the corresponding parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bef8c1b0b3744e44a8458762c04d60f4~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |explain |
   |---|---|
   |data connection name |Required item, connection name _ year, month, day, hour, second, such as ftp_sftp_xxx |
   |protocol type |FTP or SFTP<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>FTP server deployment:</strong></div><br><br><br><div data-tips="true" data-tips-type="tip">Users can build freely, but they need to open the system connection for access.</div><br><br><br><div data-tips="true" data-tips-type="tip">The FTP server needs to be configured in passive mode, and the port range needs to be large enough. The recommended value is: Number of FTP datasets \* 2</div><br><br><br><div data-tips="true" data-tips-type="tip">For more common problems during the configuration process, please refer to Appendix 2 of this document: FTP Configuration FAQ.</div><br> |
   |connection mode |Required when selecting the FTP protocol, the default is Pasv (passive mode) |
   |file type |Support csv\ txt |
   |file directory |**The FTP file content and format requirements are as follows:** <br><br><br>1. **File directory format** : **Required,**  such as/data/student<br><br>   1. Rule 1: The last directory name must be the same as the table name, in the format/data/{tableName}, such as/data/student<br><br>   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the directory where the data file is located. If there is one, the system will automatically skip it.<br><br>   3. Rule 3: It is not recommended to change the file directory. Please update the [CDP\-Data Connection] configuration item before changing to avoid abnormal data query.<br><br>   4. Rule 4: A file directory represents a table, and multiple tables sharing a file directory is not supported, nor is it supported to have multiple directories for a table<br><br>2. **File directory content:** <br><br>   1. **Data file: Required,**  only support CSV, TXT, can have multiple files, name is not limited<br><br>      1. Rule: The order of columns (fields) in the data file must be consistent with the metadata file, and the data file does not contain a header (field name line).<br><br>      2. Rule: Each time you query, pull all the data according to the file directory address (excluding subdirectory files)<br><br>      3. Rule: The total file size in a single file directory is recommended to be less than 500G.<br><br>   2. **Meta Information \*\*\*\* File: Required,**  {tableName} .yml (if there are structural changes, this file needs to be changed)<br><br>      1. Rule 1: Use to parse data files mapped to structured tables<br><br>      2. Rule 2: {tableName} is the table name, table name change is not supported, {tableName} needs to be consistent with the directory name<br><br>      3. See **Appendix 1**<br><br>   3. **Synchronization success flag file: required,**  {date} .verf, for example 20230801.verf<br><br>      1. Logic: used to mark whether the data is pushed, CDP tasks are used to build dependency logic on FTP tasks<br><br>      2. Rule 1: The file must exist, and the 20230801 file name is read when the task is executed to determine whether the data of the corresponding business date is ready<br><br>      3. Rule 2: The synchronization success file of the historical update can be preserved and deleted without affecting the judgment of the latest day<br><br>      4. Rule 3: Brush back scenario, logically does not support the retention of historical data, each time the data is pulled from FTP is pulled according to the full amount of the file directory, when brushing back, if the synchronization success flag of the historical date still exists, all data will be pulled according to the latest file, if not, the brush back task will always be Pending, unable to execute successfully |
   

4. Click on the **parse table structure** , the file directory will be parsed, data table preview display table name and field name, table name if too much, support scrolling display, the default display of the first table name field information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d11cdb2055240458c0ba08c3daad537~tplv-goo7wpa0wc-image.image) </span>


5. Click **Test Connection** to take the data source connectivity test.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4eec59bcbcc145ea8dc4385bcbe7eac6~tplv-goo7wpa0wc-image.image) </span>


6. After the test is successful, click **Save** .


<span id="20dbd7b8"></span>
# Appendix 1: File Content Format

```Plain
#Please fill in the following parameters:
### name: field name(required)
########## Field naming convention: It is necessary to ensure the uniqueness of field names; Only supports letters, numbers, and underscores starting with a letter, with a maximum of 100 characters.
### alias: field alias(optional)
########## field alias rule: There is no limit to character types, up to a maximum of 100 characters.
### type: field type(required)
########## Type rule: No specific length is required, the following types can be specified:
    # string
    # boolean
    # long
    # double
    # date
    # datetime
    # The% s in the following two types only support basic types such as int.
    #Does not support multi-layer nesting, for instance: array<array<int>>
    # array<%s>
    # map<%s,%s>
#--------------------------------------------------------------------------------

columns:
  - name: brand_id
    alias: brandid
    type: int
  - name: brand_name
    alias: brand name
    type: string
  - name: brand_desc
    alias: brand introduction
    type: string
  - name: create_time
    alias: create time
    type: date
  - name: update_time
    alias: update time
    type: date
```


<span id="8e81c2cf"></span>
# Appendix 2: Frequently Asked Questions about FTP Configuration

**Q1: FTP connection server encountered 530 login incorrect error how to solve?** 


1. The password is incorrect.

2. Check the/etc/vsftpd/vsftpd.conf configuration

   vim /etc/vsftpd/vsftpd.conf


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">See the configuration below</div>


<div data-tips="true" data-tips-type="tip">anonymous_enable=YES</div>


<div data-tips="true" data-tips-type="tip">userlist_deny = NO//See instructions below</div>


<div data-tips="true" data-tips-type="tip">userlist_enable=YES</div>


<div data-tips="true" data-tips-type="tip">userlist_file=/etc/userlist</div>


<div data-tips="true" data-tips-type="tip">seccomp_sandbox=NOlocal_enable=YES</div>


<div data-tips="true" data-tips-type="tip">pam_service_name = vsftpd//important here, some people say that ubuntu is pam_service_name = ftp, you can try it</div>


<div data-tips="true" data-tips-type="tip">Notes on the userlist file</div>


<span id="vsftpd-userlist"></span>
# <div data-tips="true" data-tips-type="tip">vsftpd userlist</div>


<span id="if-userlist-deny-no-only-allow-users-in-this-file"></span>
# <div data-tips="true" data-tips-type="tip">If userlist_deny=NO, only allow users in this file</div>


<span id="if-userlist-deny-yes-default-never-allow-users-in-this-file-and"></span>
# <div data-tips="true" data-tips-type="tip">If userlist_deny=YES (default), never allow users in this file, and</div>


<span id="do-not-even-prompt-for-a-password"></span>
# <div data-tips="true" data-tips-type="tip">do not even prompt for a password.</div>


<span id="note-that-the-default-vsftpd-pam-config-also-checks-etc-vsftpd-ftpusers"></span>
# <div data-tips="true" data-tips-type="tip">Note that the default vsftpd pam config also checks /etc/vsftpd/ftpusers</div>


<span id="for-users-that-are-denied"></span>
# <div data-tips="true" data-tips-type="tip">for users that are denied.</div>



3. <div data-tips="true" data-tips-type="tip">Check/etc/pam.d/vsftpd</div>


   <div data-tips="true" data-tips-type="tip">vim /etc/pam.d/vsftpd   </div>
   

   <div data-tips="true" data-tips-type="tip">comment out   </div>
   

   <div data-tips="true" data-tips-type="tip">#auth required pam_shells.so   </div>
   


**Q2: Linux instance uploads files to the FTP site and reports the "425 Security: Bad IP connection" error.** 

**1) Possible reasons:** 

The FTP service has two types of connections, one is a control connection and the other is a data connection. By default, the FTP server checks whether the source Internet Protocol Address of two connections is the same when transferring data. If not, the "425 Security: Wrong IP Connection" error is reported. This problem is often due to the client side of the NAT network, and the public network Internet Protocol Address associated with the NAT is multiple, resulting in two connections and inconsistent source IP.

**2) Solution:** 

Turn off Internet Protocol Address Security Check in passive mode as follows:


1. Execute the following command to edit the FTP configuration file:

2. vi /etc/vsftpd/vsftpd.conf

3. Add the following to the configuration file.

4. pasv_promisculous = yes

5. After saving and exiting, execute the following command to restart the FTP service.

6. Service vsftpd restart.
