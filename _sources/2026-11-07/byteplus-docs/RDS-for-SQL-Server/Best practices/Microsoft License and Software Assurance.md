---
title: "Microsoft License and Software Assurance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/microsoft-license-and-software-assurance"
---

This article mainly describes how to choose a license when deploying a business based on a Microsoft software environment in Byteplus's RDS for SQL Server.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Here, I would like to remind you that you should choose genuine software based on your own business needs and strictly abide by the terms of use and authorization of the relevant products. This article is for reference only and is not a legally binding opinion. Please do not rely solely on it. Microsoft's genuine software is renowned for its high performance, high stability, and high security. If you have any questions or confusion about the licensing and related rights of Microsoft's genuine software, it is recommended that you promptly consult your legal team, professional law firm, Microsoft official channels or relevant distributors for accurate answers and guidance.</div>


<span id="term-explanation"></span>
## term explanation


|noun |explain |
|---|---|
|Microsoft license |The Microsoft License is a legal document issued by Microsoft to users, which stipulates the user's conditions and rights to use Microsoft software. Details can be found in [Microsoft Licensing](https://www.microsoft.com/en-us/Licensing). |
|Software Assurance |Software Assurance is a comprehensive program offered by Microsoft to provide users with a unique set of technologies, services, and benefits to help them use Microsoft products effectively. Details can be found in [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default). |


<span id="use-the-license-officially-provided-by-byteplus"></span>
## Use the license officially provided by Byteplus

Byteplus is granted access to Microsoft licenses through Microsoft's [Service Provider License Agreement](https://www.microsoft.com/licensing/docs/view/Services-Provider-License-Agreement-SPLA)(SPLA). Therefore, the Windows Server public image provided by Byteplus and its pre\-installed SQL Server database are licensed for compliance. RDS for SQL Server instances that use Windows Server public mirrors do not require a separate client side access license (CAL). Each Windows instance comes with two remote connections by default for administrative purposes only. If you need more than two remote connections, or need to use these remote connections for purposes other than administration, you will need to introduce an additional client side access license for Remote Desktop Services (Remote Desktop Services CAL).

<span id="use-of-bring-your-own-license-byol"></span>
## Use of bring your own license (BYOL)

If you already have a Microsoft license, you can open a RDS for SQL Server BYOL specification instance, enter the license into the created RDS for SQL Server BYOL instance, and use your own license (BYOL) in RDS for SQL Server.

Please confirm whether your license purchases Software Assurance services, see [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default) for details.

Currently creating and using instances of RDS for SQL Server BYOL specifications is a whitening function. To use it, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.
