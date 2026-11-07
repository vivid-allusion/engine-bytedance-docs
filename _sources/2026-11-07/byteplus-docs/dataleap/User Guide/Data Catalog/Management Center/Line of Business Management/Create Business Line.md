---
title: "Create Business Line"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Create_Business_Line"
---

A business line is a collection of businesses with the same attributes, usually corresponding to functional departments within a company. In the asset portal construction scenario, it refers to the production and management unit of related data assets and documents under the asset catalog and asset album.

<span id="430bddf6"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Management Center \> BusinessLine Management** to enter the **BusinessLine Management** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5313c9a822774bc4b3568f78fae41d49~tplv-goo7wpa0wc-image.image) </span>

3. Click the **Add Business Line** button. In the pop\-up window, set the business line information, then click **OK** to complete the creation.

   The following table explains the related parameters for creating a business line. Parameters marked with \* are required; those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |**Basic Information** ||
   |\*Business line name |The name of the business line, set by the user. Supports Chinese characters, letters, numbers, underscore "_", hyphen "\-", and blank space; must begin with a Chinese character, letter, or number.<br><br>The business line name must be unique and cannot be changed once set. |
   |\*Description |Business line description information. |
   |\*Admin |The business line admin defaults to the current user but can be selected from other users; multiple selections are allowed.<br><br>Becoming a business line admin grants all functional permissions under the business line.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The main account is by default the BusinessLine Administrator and cannot be deleted. If no main account is selected, the user will be automatically added as an admin once the business line is created successfully.</div><br> |
   |Mandatory Modeling Specification |You can choose whether to enforce mandatory modeling specifications when creating tables under this business line.<br><br>If **Yes** is selected, data hierarchy, modeling specification category, and storage policy become required fields when creating tables; table names will automatically include the corresponding prefix and suffix. |
   |Business Line Data Hierarchy |The business line includes data layers. The dropdown allows multiple selections from the following options. Supports rapid selection by searching keyword in the layer name.<br><br><br>* Operational data store (ods)<br><br>* Data integration layer (dwi)<br><br>* Basic dimensions layer (dim)<br><br>* Detailed data layer (dwd)<br><br>* Intermediate data layer (dwm)<br><br>* Data warehouse service layer (dws)<br><br>* data warehouse application layer (dwa)<br><br>* Data market layer (dm)<br><br>* Application Service Layer (ads)<br><br>* Application Layer (app) |
   |Enable data hierarchy and storage policy cascading |You can choose whether to enable cascading for data hierarchy and storage policy. |
   |Data\-Level associative Storage Policy |After enabling cascading for data hierarchy and storage policy, set the association between data hierarchy and storage policy. Multiple sets are supported.<br><br>Each set contains the following information:<br><br><br>* Data hierarchy: Dropdown to select the **business line data hierarchy** that has been chosen.<br><br>* Storage policy: Management policies for the business line's data hierarchy. Multiple selectable storage policies are available in the dropdown.<br><br>   * minute increment (mi)<br><br>   * hour increment (hi)<br><br>   * daily increment (di)<br><br>   * minute full (mf)<br><br>   * hour full (hf)<br><br>   * daily full (df) |
   |modeling user strong control |optionally apply modeling user strong control.<br><br>when **yes** is selected, set managing members and control departments. |
   |modeling control members |members controlling modeling data; enter account keywords to select from dropdown, multiple selections supported. |
   |Modeling control department |The department controlling modeling data. Enter department names; multiple entries supported and optional. |
   |Asset Operator |Operators of the line of business assets. Enter account keywords to select from a dropdown; multiple selections supported. |
   |\*Hidden |Option to hide the line of business.<br><br>If you select **Yes**, the line of business is visible only to line\-of\-business administrators in My Assets, Asset Catalog, Asset Album, Asset Management, and related modules. |
   |**Custom Information \- Default Sorting Settings** ||
   |Asset Catalog Default Sort |Default sorting rules for the asset catalog. The dropdown allows multiple selections and custom sorting. In the **Asset Catalog** module, search results are sorted by default according to specified settings.<br><br><br>* Creation time<br><br>* Update time<br><br>* Heat<br><br>* Shelf time<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When keyword match levels are equal, sorting is performed according to the specified dimension. Dimensions positioned earlier have higher priority.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are no search keywords (that is, by default entering the Asset Catalog or Album modules), the specified default sorting dimension determines the asset display order.</div><br> |
   |Asset Album Default Sort |Default sorting rules for asset albums. The dropdown allows multiple selections and custom sorting.<br><br><br>* Creation time<br><br>* Update time<br><br>* Heat<br><br>* shelf time<br><br><br>In the **Asset Album** module, search results default to the specified sort settings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When keyword match levels are equal, sorting is performed according to the specified dimension. Dimensions positioned earlier have higher priority.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When there are no search keywords (that is, by default entering the Asset Catalog or Album modules), the specified default sorting dimension determines the asset display order.</div><br> |
   |**Custom information \- default category publishing policy settings** ||
   |Published asset management strategy |You can choose whether to allow editing or categorization.<br><br>When enabled, published assets support manual direct editing, categorization, and direct posting; otherwise, editing and categorization require removal first. |
   |**Custom information \- asset display settings** (configuration for asset display on the **Asset Catalog** page.) ||
   |Asset Catalog Display Assets and Sequence |Users can choose whether to display the corresponding asset types and their display order on the **Asset Catalog** page as needed. If empty, it defaults to follow system settings. |
   |Theme Directory Settings |The display method of the business line theme directory on the **Asset Catalog** page, currently has the following two options:<br><br><br>* Single theme directory: Display using the business line name as the theme directory.<br><br>* Multi\-theme directory: Supports classification display by category as the theme directory. |
   |Default Category Theme |The business line theme directory displayed by default on the **Asset Catalog** page. The default option is **Comprehensive Catalog**, selectable from the dropdown. If empty, it defaults to follow system settings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>theme directory settings</strong> selects <strong>multi\-theme directory</strong>, this parameter can be set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the business line configures data classification categories, the dropdown options under this parameter will display the corresponding theme options. You can modify the default category theme as needed when editing the business line.</div><br> |
   |Search for unlisted assets |Choose whether to support searching for unlisted assets under the business line on the **Asset Catalog** page. Support option **Allow search for unlisted assets**, checked by default and editable. |
   |Search for off\-shelf assets |Choose whether to support searching for off\-shelf assets under the business line on the **Asset Catalog** page. Support option **Allow search for off\-shelf assets**, checked by default and editable. |
   |Search the assets of the whole site |Choose whether to support searching site\-wide assets on the **Asset Catalog** page. Support option **Allow to search the assets of the whole site**, checked by default and editable. |
   |Site\-wide & business line tab sorting |The display order of the site\-wide Tab and the business line Tab on the **Asset Catalog** page supports the following options, selectable from the dropdown:<br><br><br>* Site\-wide/Business line: Site\-wide first, business line second.<br><br>* Business line/Site\-wide: Business line first, site\-wide second. |
   |Site\-wide asset display name |The site\-wide Tab display name on the **Asset Catalog** page, shown as the set Chinese name. Default is set to **Site\-wide assets**, modifiable as needed. |
   |Line of Business Tab Display Name |The business line Tab display name on the **Asset Catalog** page, shown as the set Chinese name. If empty, it defaults to follow the system settings. |
   


<span id="8e5ab6ea"></span>
## Operation Result

After configuring the asset display settings in the custom message section, the [Asset Catalog](https://docs.byteplus.com/docs/dataleap/Asset_Catalog)page will display accordingly.

<span id="e107beaa"></span>
## Subsequent Operations

After creating a business line, you can manage categories, albums, assets, tags, and other configurations under it. For related operations, see [Asset Management](https://docs.byteplus.com/en/docs/dataleap/Asset_Management).
