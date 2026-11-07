---
title: "Create authorization code (share-crt)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-authorization-code-share-crt"
---

You can create an authorization code for the object to be shared using the `share-crt` command.

<span id=".5ZG95Luk5qC85byP"></span>
## Command format


<Tabs>
<Tab zoneid="RAQ18Jw0" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil share-crt tos://bucket[/prefix] [-vp=xxx] [-dst=xxx] [-em] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="nnpeHXaG" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil share-crt tos://bucket[/prefix] [-vp=xxx] [-dst=xxx] [-em] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For the description of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket containing the object to share. |
|prefix |String |The object name prefix to share is explained as follows:<br><br><br>* If the value is empty: It means sharing all objects in the bucket.<br><br>* If the value is not empty: It means sharing all objects starting with this prefix.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When setting this parameter, it is recommended to end with <code>/</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to browse shared objects with the specified prefix through a browser or the TOS Browser tool, this parameter must end with <code>/</code>.</div><br> |
|\-vp |String |Set the validity period for the authorization code, with a range from 1 minute to 7 days. If you configure the tosutil tool using temporary access keys, the maximum selectable validity period of the authorization code aligns with the expiration time of the temporary access keys.<br><br>The default value is 1 day, meaning the generated authorization code expires 1 day later. This parameter supports the following configuration methods:<br><br><br>* w: Sets the unit to weeks.<br><br>* d: Sets the unit to days.<br><br>* h: Sets the unit to hours.<br><br>* min: Sets the unit to minutes.<br><br>* s: Sets the unit to seconds.<br><br><br>For example, `1d` means a validity period of 1 day, `1w` means 1 week, and `1h` means 1 hour.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify a time unit, the default unit is seconds. For example, <code>2400</code> means a validity period of 2,400 seconds.</div><br> |
|\-dst |String |Path to save the authorization code. |
|\-em |Bool |Set exact match to share only a single object. |


<span id=".5L2_55So56S65L6L"></span>
## Example

<span id="52e5da03"></span>
### Share all objects in the bucket

The following command shares all objects in the **bucketname** bucket with an authorization code valid for 1 hour.


* Command

   ```bash
   ./tosutil share-crt tos://bucketname -vp 1h
   ```
   

* Output

   ```plain
   Authorization Code:
   https://document-share.tos-cn-beijing.bytepluses.com.cn/index.html?token=/****+aY3yfy+JmQ2Yd144VAZ5FuFbHru0ADVaY5wZkCUQMZYifSKe5n1IL2WqrqLb/bzYMKl2lqdIZPG8dBL4XEXeKE9SqtS4n+f17aaSIBU3B288ly9ANNBJ7eaBCni7/UKKpK49ZfXxm0mCdbS9sFTNahK5IAesDvAqMQis7wTxRrrqSRG2zGgabYgTNbRWD2OklttTJPtSA4940kisfHOEQwWBZol7MVarJItDqVEeiT80wLa3pr+5gb/8ZtWrBBfCOjAkEJY7AUmOSm5IMJsbhIzRhk9nV9ieDfSvJBGFaFg+vBjF7Xut2/pAEKozR2lKCoCKKZwI9BOJMnlCd15e9vlQfNeUVARqfhyTrVJJzX3wJfB/KTiA1MPQRtogaANfeHgOtPxu2gQzdPFX5kbRXAMmIEQHxZ/zOPR52AEWJSKLwDU/McV101wKuGIiQr90rs2izlMuEywF7g+cXftUmMvaMDQWehRpMRpxlI8kZMwVwJ/pbt3wi3/sNFgoSnnzvHxXY8dF/WsqVLUxOec3Qrd7l96bCY3Pd3yc742Mk7PO+VLOMIB//k****
   
   Valid Until:
   Tue, 06 Dec 2022 10:45:50 GMT
   ```
   


<span id="c91eef37"></span>
### Share a specific directory within the bucket

The following command shares objects in the **bucketname** bucket's **file** folder.


* Command

   ```bash
   ./tosutil share-crt tos://bucketname/file/
   ```
   

* Output

   ```plain
   Authorization Code:
   https://document-share.tos-cn-beijing.bytepluses.com.cn/index.html?token=/****+aY3yfy+JmQ2Yd144VAZ5FuFbHru0ADVaY5wZkCUQMZYifSKe5n1IL2WqrqLb/bzYMKl2lqdIZPG8dBL4XEXeKE9SqtS4n+f17aaSIBU3B288ly9ANNBJ7eaBCni7/UKKpK49ZfXxm0mCdbS9sFTNahK5IAesDvAqMQis7wTxRrrqSRG2zGgabYgTNbRWD2OklttTJPtSA4940kisfHOEQwWBZol7MVarJItDqVEeiT80wLa3pr+5gb/8ZtWrBBfCOjAkEJY7AUmOSm5AfYxAXhJzE8QbKWhGZiLCzxD7N7cXUZuwLJ5NrM7Q9X06OxXwYoBDrS35B+3DEkjPBqI1AM/H9AFj62jTj35j4r83p8bWsElBcCiut8Vvdw7QXWiICDyFnNcmYR7C5J/iYUXhh9uDH7pjfeZkbKkV5heNwTIoA2Q3GozRPv966ktNJRBw0zN++P8n9ER7aRV7MgsoevwBQQCeC/KA47lQ34nf6uMmGum2wVIe9b4PCPoAOrYPW8h0eKfhnmkHLJEhaKPhvZISBH+9BQriBln73ASwbDt92FWwOqNF/vOH8UsxCsLzUxPd686st0PSSs****
   
   Valid Until:
   Tue, 06 Dec 2022 10:47:17 GMT
   ```
   


<span id="243f8769"></span>
### Share a specific directory within the bucket and specify the authorization code save path

The following command shares objects in the **bucketname** bucket's **file** folder, with the authorization code path set to  **/tmp/tosutil/authorization_code** and a validity of 2 hours.


* Command

   ```bash
   ./tosutil share-crt tos://bucketname/file/ -dst=/tmp/tosutil/authorization_code -vp=2h
   ```
   

* Output

   ```plain
   The result is generated to [/tmp/tosutil/authorization_code]
   ```
   


<span id="351889ed"></span>
### Share a single object within the bucket

The following command shares the **object1.png** object within the **bucketname** bucket.


* Command

   ```bash
   ./tosutil share-crt tos://bucketname/object1.png -em
   ```
   

* Output

   ```plain
   Authorization Code:
   https://document-share.tos-cn-beijing.bytepluses.com.cn/index.html?token=/****+aY3yfy+JmQ2Yd144VAZ5FuFbHru0ADVaY5wZkCUQMZYifSKe5n1IL2WqrqLb/bzYMKl2lqdIZPG8dBL4XEXeKE9SqtS4n+f17aaSIBU3B288ly9ANNBJ7eaBCni7/UKKpK49ZfXxm0mCdbS9sFTNahK5IAesDvAqMQis7wTxRrrqSRG2zGgabYgTNbRWD2OklttTJPtSA4940kisfHOEQwWBZol7MVarJItDqVEeiT80wLa3pr+5gb/8ZtWrBBfCOjAkEJY7AUmOSm5DKH9vSYHHsx/NyPU4pOITmYALY8oDS2RmyGLwKV2MGv0dZSMViKFFVYn8M2mjXeadd1uvOFhXRjgj3jn1sJzyca9cgeCgH93dI6Tpa/DvZRdVY1IUhuCEX3ast2dhhsbSdzhmcV4PJ0jfxIvjdEGhYbp8wbfXVwJ028DBsvToRFpSIbr5fvYPAb2y7Wxp0AdXdUKXdWOtE2Ui9o+A8frSKcSAQxvW2EBLKoaL9GWQdrXhaYZtCLqd0TcOqr2d5GjuyJiMzqf9i5Wu98ydLsEYBiN8t1pbKOXuNMDbK/****
   
   Valid Until:
   Tue, 06 Dec 2022 10:48:12 GMT
   ```
