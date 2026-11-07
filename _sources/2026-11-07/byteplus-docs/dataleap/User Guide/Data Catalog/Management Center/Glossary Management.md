---
title: "Glossary Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Glossary_Management"
---

The business glossary provides vocabulary for business users. It allows terms to be linked and maps terms to data assets such as databases, tables, datasets/kanbans, and albums, helping users discover, understand, and use data through terminology. Each business term represents a unified industry name for certain specific entities within a particular domain. This feature lets you create and manage business terms. This document explains how to operate it.

<span id="7fa7761e"></span>
## Constraints


* Only the term owner can create lower\-level terms under their responsible terms, with a maximum hierarchy of four levels.

* Only the term owner can edit or delete the terms they are responsible for, as well as all subordinate terms under them.


<span id="994cc3c7"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Management Center \> Glossary Management** to enter the glossary management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b77d480662da489aa44075307faa5e2a~tplv-goo7wpa0wc-image.image) </span>

3. Click the **Business glossary** directory's **New Term** button, set the term information, then click the **Create** button to complete the creation of a top\-level term.

   The table below explains the parameters related to creating a term.

   
   |Parameters |Description |
   |---|---|
   |Term name |Name of the business term, set as needed.<br><br>The term name starts with Chinese, English letters, or numbers, and consists of Chinese, English letters, numbers, underscores, or &; the length does not exceed 50 characters. |
   |Higher\-level term |The higher\-level term of this term, selectable from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only higher\-level business terms for which you are the owner may be selected. If you cannot find the desired higher\-level business term, contact the owner of that term to add you as an owner before you can select it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When creating a top\-level business term, selecting a higher\-level term is not required.</div><br> |
   |Owner |The owner of this term, default is the current user. Enter keywords to select accounts under the current tenant from the dropdown; multiple selections supported. |
   |Description |Description of this business term for management, with a maximum length of 500 characters. |
   

4. The following operations are also available:

   * Hover the mouse over a created term to create or delete terms.

      * Click the  **︙ \> New Term** button to create a lower\-level term under that term.

      * Click the  **︙ \> Delete term** button, and confirm to delete the term.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">This business term can only be deleted after all its lower\-level terms have been removed.         </div>
         

   * Click to select a created term to enter its information page, where you can view term details and perform the following operations:

      * Click the **New Term** button to create a lower\-level term.

      * Click the  **︙ \> Edit terms** button to modify the term.

      * Click the  **︙ \> Delete term** button and confirm again to delete the term.

      * Click the **Associate data** tab to view data related to the term.

      * Click the **Lower\-level term** tab to view the next\-level terms and perform delete, edit, or view actions.

      * Click the **Change history** tab to view the list of information changes for the term.

   * Enter the term name keyword in the search box of the **Business glossary** directory to find matching terms.


<span id="01782ba8"></span>
## Subsequent Actions

After creating a business term, on the **Table Management** page, when creating and managing data tables, you can associate terms with the tables; see [Table Management](https://docs.byteplus.com/en/docs/dataleap/Table_Management) for related operations.
