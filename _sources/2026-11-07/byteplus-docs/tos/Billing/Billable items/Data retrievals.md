---
title: "Data retrievals"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-data-retrieval-fee"
---

Accessing files in Infrequent Access Storage, Flashback Archive, or another storage type incurs the data retrieval fee. This topic describes only details about billable items.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes only details about billable items. For more information on pricing, see <a href="https://www.byteplus.com/en/pricing?product=TOS&tab=1">TOS pricing</a>.</div>



|**Billable Item** |**Description** |**Formula** |
|---|---|---|
|Infrequent Access Storage \- Data retrievals |You are charged based on the volume of data retrieved when accessing a file stored in Infrequent Access Storage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you send HTTP Range requests to read certain parts of a file, the volume of retrieved parts is the number of retrieved bytes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you access the file in other ways, the volume of retrieved data is the actual file size.</div><br> |**Pay\-as\-you\-go**: Data retrieval cost = Volume retrieved (GiB) × Price per GiB |
|Flashback Archive \- Data retrievals |You are charged based on the volume of data retrieved when accessing a file stored in Flashback Archive.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can retrieve data from Flashback Archive without restoration.</div><br> |**Pay\-as\-you\-go**: Data retrieval cost = Volume retrieved (GiB) × Price per GiB |
|Archive \- Data retrievals |You need to restore files in Archive before reading them, which incurs retrieval costs.<br><br>Retrievals typically finish within one minute for files stored in Archive. |**Pay\-as\-you\-go**: Data retrieval cost = Volume retrieved (GiB) × Price per GiB |
|Cold Archive \- Data retrievals |You need to restore files in Cold Archive before reading them, which incurs retrieval costs. The unit price for data retrieval varies depending on the restoration time. Shorter restoration times result in higher unit prices. Restoration options are as follows:<br><br><br>* Quick: 1–5 minutes<br><br>* Standard: 2–5 hours<br><br>* Batch: 5–12 hours |**Pay\-as\-you\-go**: Data retrieval cost = Volume retrieved (GiB) × Price per GiB |
|Deep Cold Archive \- Data retrievals |You need to restore files in Deep Cold Archive before reading them, which incurs retrieval costs. The unit price for data retrieval varies depending on the restoration time. Shorter restoration times result in higher unit prices. Restoration options are as follows:<br><br><br>* Standard: Within 12 hours<br><br>* Batch: Within 48 hours |**Pay\-as\-you\-go**: Data retrieval cost = Volume retrieved (GiB) × Price per GiB |
