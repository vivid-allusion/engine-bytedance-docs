---
title: "Chemical molecular calculation retrieval (RDKit)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/RDKit"
---

RDKit is an open\-source cheminformatics toolkit that uses machine learning methods to generate compound fingerprints for compound substructure searches and structural similarity calculations.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions

Supports the use of RDKit extension only in PostgreSQL 13 and above versions, see [Supported extension list](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_supported_plugins) for the version of extension needed to be used in each version instance.

<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
### Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

```sql
CREATE EXTENSION rdkit;
```



* Delete extension


```sql
DROP EXTENSION rdkit;
```


<span id=".5pWw5o2u57G75Z6L"></span>
### Data type


* **Data type description**

   The basic data types supported by the extension are `mol`, `qmol`, `bfp`, `sfp`, and `reaction`. The meanings of different types are as follows:

   * `mol` is a commonly used chemical molecule format, usually used to save a single molecule.

   * `qmol` is a chemical molecule data type containing query features provided by RDKit, which can be directly transformed from formats such as `SMARTS` to `qmol` type data, for example `‘c1cccc[c,n]1’::qmol`.

   * `bfp` is a bit vector form of chemical molecular fingerprint type provided by RDKit.

   * `sfp` is a sparse vector form of chemical molecular fingerprint type provided by RDKit.

   * `reaction` is a chemical reaction template type provided by RDKit.

* **Data type conversion**

   * Convert `SMILES` format molecules into `mol` type and insert into the table.

      ```sql
      insert into mols values
      (1, 'C1=CC=C\\2C(=C1)C=CC(=O)/C2=N\\NC3=NC=CS3'::mol),
      (2, 'CC1=C(N=CC=C1)NC2=NC(=CS2)C3=CC=CC=N3'::mol),
      (3, 'CC(=NNC1=C(C=C(C=N1)Cl)Cl)C2=CC=CC=N2'::mol),
      (4, 'CC(=NNC(=S)NCC=C)C1=CC=CC=N1'::mol),
      (5, 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);
      ```
      

   * Convert `SMARTS` format molecules into `qmol` type.

      ```sql
      select 'c1[o,s]ncn1'::qmol;
      ```
      

   * Use fingerprint calculation function to convert `mol` type data into `sfp` type data, and insert into the table.

      ```sql
      select id, torsion_fp(m) as tfp, morgan_fp(m) as mfp, featmorgan_fp(m) as ffp into sfps from mols;
      ```
      

   * Use fingerprint calculation functions to convert` mo`l type data into` bf`p type data, and insert them into the table.

      ```sql
      select id, torsionbv_fp(m) as tfp, morganbv_fp(m) as mfp, featmorganbv_fp(m) as ffp into bfps from mols;
      ```
      

   * Convert the `SMARTS` format chemical reaction template into a `reaction` object (chemical reaction engine object).

      ```sql
      SELECT reaction_from_smarts('c1ccc[n,c]c1>>c1nccnc1');
      ```
      


<span id=".5pON5L2c56ym"></span>
### Operators

This topic uses `mol` type and `bfp` type as examples to explain the meaning and usage of operators, the meaning and usage of each operator under other data types are basically consistent with `mol` type and `bfp` type, this topic will not list them one by one. Refer to [RDKit user guide](https://www.rdkit.org/docs/Cartridge.html#reference-guide) for more details.

<span id=".bW9sIOexu-Weiw=="></span>
#### `mol` type

`mol` type supports substructure query operators (`<@`, `@>`, `@=`) and comparison operators (`>`, `>=`, `<`, `<=`, `<>`, `=`). The meanings and uses of various operators when handling `mol` type objects are as follows:


|Operators |Note |Examples |
|---|---|---|
|`<@` |`mol1` `<@` `mol2`:<br><br>Return true if mol1 is a substructure of mol2, otherwise return false. |```sql```<br>```-- Query the mols table for molecules containing the 'c1cccnc1' structure```<br>```select * from mols where 'c1cccnc1'::mol <@ m;```<br>```-- Query the molecules in the mols table that are substructures of 'c1cccnc1'```<br>```select * from mols where m <@ 'c1cccnc1'::mol;```<br> |
|`@>` |`mol1` `@>` `mol2`:<br><br>Return true if mol2 is a substructure of mol1, otherwise return false. |```sql```<br>```-- Query the molecules in the mols table that are substructures of 'c1cccnc1'```<br>```select * from mols where 'c1cccnc1'::mol @> m;```<br>```-- Query the mols table for molecules containing the 'c1cccnc1' structure```<br>```select * from mols where m @> 'c1cccnc1'::mol;```<br> |
|`<@` |`qmol` `<@` `mol`:<br><br>Return true if qmol is a substructure of mol, otherwise return false. |```sql```<br>```-- Query the mols table for molecules containing the 'c1cccnc1' structure```<br>```select * from mols where 'c1cccnc1'::qmol <@ m;```<br> |
|`@>` |`mol` `@>` `qmol`:<br><br>Return true if qmol is a substructure of mol, otherwise return false. |```sql```<br>```-- Query the mols table for molecules containing the 'c1cccnc1' structure```<br>```select * from mols where m @> 'c1cccnc1'::qmol;```<br> |
|`@=` |`mol1` `@=` `mol2`: Return true if mol1 and mol2 have the same structure, otherwise return false. |```sql```<br>```-- Query the mols table for molecules that have the same structure as 'C=CCNC(=S)NN=C(C)c1ccccn1'```<br>```select * from mols where m @= 'C=CCNC(=S)NN=C(C)c1ccccn1'::mol;```<br> |
|`>` |`mol1` `>` `mol2`: Return true if mol1 is greater than mol2; otherwise, return false. |```sql```<br>```-- Query the mols table for molecules greater than 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m > 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |
|`>=` |`mol1` `>=` `mol2`: Return true if mol1 is greater than or equal to mol2, otherwise return false. |```sql```<br>```-- Query the mols table for molecules greater than or equal to 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m >= 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |
|`<` |`mol1` `<` `mol2`: Return true if mol1 is less than mol2; otherwise, return false. |```sql```<br>```-- Query the mols table for molecules less than 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m < 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |
|`<=` |`mol1` `<=` `mol2`: Return true if mol1 is less than or equal to mol2, otherwise, return false. |```sql```<br>```-- Query the mols table for molecules that are less than or equal to 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m <= 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |
|`<>` |`mol1` `<>` `mol2`: Return true if mol1 does not equal mol2, otherwise return false. |```sql```<br>```-- Query the mols table for molecules that are not equal to 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m <> 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |
|`=` |`mol1` `=` `mol2`: Rreturn true if mol1 equals mol2, otherwise return false. |```sql```<br>```-- Query the mols table for molecules that are equal to 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'```<br>```select * from mols where m = 'CC(=NNc1ncc(Cl)cc1Cl)c1ccccn1'::mol;```<br> |


&nbsp;

<span id=".YmZwIOexu-Weiw=="></span>
#### `bfp` type

`bfp` type supports similarity query operators (`%`, `<%>`, `#`, `<#>`) and comparison operators (`>`, `>=`, `<`, `<=`, `<>`, `=`). The meanings and usages of different operators when operating on `bfp` type objects are shown in the following table:


|Operators |Note |Examples |
|---|---|---|
|`%` |`bfp1` `%` `bfp2`:<br><br>Return true if the Tanimoto similarity of bfp1 and bfp2 exceeds the threshold, otherwise return false. |```sql```<br>```-- Query the Tanimoto similarity between molecules in the bfps table and 'c1cccnc1'.```<br>```select id, tanimoto_sml(morganbv_fp('c1cccnc1'::mol) , mfp) from bfps;```<br>```-- Query whether the Tanimoto similarity between molecules in the bfps table and 'c1cccnc1' exceeds the threshold.```<br>```select id, morganbv_fp('c1cccnc1'::mol) % mfp from bfps;```<br> |
|`<%>` |`bfp1` `<%>` `bfp2`:<br><br>Return the Tanimoto similarity distance between bfp1 and bfp2, commonly used for sorting. |```sql```<br>```-- Query the Tanimoto similarity distance between molecules in the bfps table and 'c1cccnc1'```<br>```select id, morganbv_fp('c1cccnc1'::mol) <%> mfp from bfps order by morganbv_fp('c1cccnc1'::mol) <%> mfp;```<br> |
|`#` |`bfp1` `#` `bfp2`:<br><br>Return true if the Dice similarity between bfp1 and bfp2 exceeds the threshold, otherwise return false. |```sql```<br>```-- Query the Dice similarity with 'c1cccnc1' in the bfps table```<br>```select id, dice_sml(morganbv_fp('c1cccnc1'::mol), mfp) from bfps;```<br>```-- Check whether the Dice similarity between molecules in the bfps table and 'c1cccnc1' exceeds the threshold```<br>```select id, morganbv_fp('c1cccnc1'::mol) # mfp from bfps;```<br> |
|`<#>` |`bfp1` `<#>` `bfp2`:<br><br>Return the Dice similarity distance between bfp1 and bfp2, usually used for sorting. |```sql```<br>```-- Query the Dice similarity distance between molecules in the bfps table and 'c1cccnc1'```<br>```select id, morganbv_fp('c1cccnc1'::mol) <#> mfp from bfps order by morganbv_fp('c1cccnc1'::mol) <#> mfp;```<br> |
|`>` |`bfp1` `>` `bfp2`: Return true if bfp1 is greater than bfp2, otherwise return false. |```sql```<br>```-- Query the bfps table for molecules greater than 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp > morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |
|`>=` |`bfp1` `>=` `bfp2`: Return true if bfp1 is greater than or equal to bfp2; otherwise, return false. |```sql```<br>```-- Query the bfps table for molecules greater than or equal to 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp >= morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |
|`<` |`bfp1` `<` `bfp2`: Return true if bfp1 is less than bfp2, otherwise return false. |```sql```<br>```-- Query the mols table for molecules less than 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp < morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |
|`<=` |`bfp1` `<=` `bfp2`: Return true if bfp1 is less than or equal to bfp2; otherwise, return false. |```sql```<br>```-- Query the mols table for molecules that are less than or equal to 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp <= morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |
|`<>` |`bfp1` `<>` `bfp2`: Return true if bfp1 does not equal bfp2; otherwise, return false. |```sql```<br>```-- Query the mols table for molecules that are not equal to 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp <> morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |
|`=` |`bfp1` `=` `bfp2`: Return true if bfp1 equals bfp2; otherwise, return false. |```sql```<br>```-- Query the mols table for molecules equal to 'CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'```<br>```select id, mfp from bfps where mfp =  morganbv_fp('CC1=CC=C(C=C1)C(=O)SC2=CC=CC=CC2=O'::mol);```<br> |


&nbsp;

<span id=".5Ye95pWw"></span>
### Functions

RDKit supports a wide range of functions, but this section only provides a simple demonstration of their calling. For more detailed information, refer to the [RDKit Usage Guide](https://www.rdkit.org/docs/Cartridge.html#reference-guide).


* `tanimoto_sml(bfp, bfp)`: Calculates Tanimoto similarity.

   ```sql
   postgres=# select tanimoto_sml(morganbv_fp('c1cccnc1'::mol), morganbv_fp('c1cccnc1'::mol));
    tanimoto_sml
   --------------
               1
   (1 row)
   
   postgres=# select tanimoto_sml(morganbv_fp('C1C(OC2=CC(=CC(=C2C1=O)))'::mol), morganbv_fp('c1cccnc1'::mol));
       tanimoto_sml
   ---------------------
    0.06666666666666667
   (1 row)
   ```
   

* `dice_sml(bfp, bfp)`: calculates `dice` similarity.

   ```sql
   postgres=# select dice_sml(morganbv_fp('c1cccnc1'::mol), morganbv_fp('c1cccnc1'::mol));
    dice_sml
   ----------
           1
   (1 row)
   
   postgres=# select dice_sml(morganbv_fp('C1C(OC2=CC(=CC(=C2C1=O)))'::mol), morganbv_fp('c1cccnc1'::mol));
    dice_sml
   ----------
       0.125
   (1 row)
   ```
   


<span id=".57Si5byV"></span>
## Index

RDKit supports btree index, gist index, and gin index. Below is a description of how to use various indexes, exemplified by the `bfp` type.


* Create btree index

   ```sql
   -- Create btree index
   drop index if exists bfpidx;
   create index bfpidx ON bfps(tfp);
   ```
   

* Create gist index

   ```sql
   -- Create gist index
   drop index if exists bfpidx;
   create index bfpidx on bfps using gist(tfp);
   ```
   

* Create gin index

   ```sql
   -- Create gin index
   drop index if exists bfpidx;
   create index bfpidx on bfps using gin(tfp);
   ```
   


<span id=".5Y-C6ICD5paH5qGj"></span>
## References

[RDKit user guide](https://www.rdkit.org/docs/Cartridge.html#reference-guide)
