---
title: "Enabling row-level security (RLS)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/RLS"
---

Row\-level security (RLS) is a data access control mechanism provided by PostgreSQL. After enabling RLS, you can control access permissions to rows in a table for different users by writing policies, achieving row\-level data isolation.

In the AI Native BaaS for Supabase, it is recommended to enable RLS for all tables containing user data. After enabling RLS, if no policy is created, querying the table through the Supabase API will return empty results, ensuring data is inaccessible by default.

<span id="PqncfXZt"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="B0iKKDp6"></span>
## Procedure

You can enable RLS in two ways.

<span id="yDb10P13"></span>
### Method one: enable RLS when creating a table


1. Log in to the Supabase console and enter the target project.

2. Select **Table Editor** in the left navigation bar.

3. Click **New table**, then fill in the table name, description, and other information in the pop\-up dialog.

4. Check the **Enable row level security (RLS)**  checkbox (marked as recommended).

5. Click **Save** to save the table.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only enable RLS when creating the table. After saving the table, go to the <strong>Authentication \> Policies</strong> page to create access policies. Otherwise, querying the table through the API will return empty results.   </div>
   

<span id="6x5B6WDo"></span>
### Method two: enable RLS on the policies page

For existing tables without RLS enabled, you can enable it uniformly on the policies page.


1. Select **Authentication** in the left navigation bar.

2. Under the **CONFIGURATION** section, select **policies**.

3. Find the target table in the table list. Tables with RLS disabled will display the **RLS Disabled** tag.

4. Click the **Enable RLS** button corresponding to the table.

   After enabling successfully, the button changes to **Disable RLS**, allowing you to disable RLS at any time using this button.


<span id="dfpAyrFi"></span>
## Instructions

<span id="pYgcUQH3"></span>
### Create access policy

After enabling RLS, you need to create policies for the table to allow users to access data properly.


1. Enter the **Authentication \> Policies** page.

2. Find the target table with RLS enabled and click **Create policy**.

3. Configure the policy Name, target roles, and USING expression based on business requirements. For INSERT and UPDATE operations, also configure the WITH CHECK expression.

4. After saving the policy, users who meet the conditions can access the corresponding rows via API.


<span id="WEyYm6JP"></span>
#### Explanation of fields in the Create Policy popup

In the **Create a new Row Level Security policy** popup, the form is on the left, and common policy templates (Template list) are on the right. The fields are explained as follows.

**Form fields on the left side**


* **Policy name**: strategy name, customize as needed.

* **Table** (on clause): target table for this strategy, in schema.tableName format, e.g., public.xinli.

* **Policy behavior** (as clause): type of policy behavior, selected from dropdown.

   * **Permissive**: access allowed if any permissive policy matches (OR logic).

   * **Restrictive**: all restrictive policies must be satisfied for access (AND logic).

* **Policy command** (for clause): operation type this policy applies to, single choice; options include SELECT, INSERT, UPDATE, DELETE, ALL.

* **Target roles** (to clause): roles this policy applies to; by default, applies to all (public) roles; specific roles can be designated.


The SQL editor below the form displays an automatic preview of the policy SQL generated from the above fields; you can directly edit USING and WITH CHECK expressions here.

**Template list on the right**

The popup’s right side offers common policy templates; click a template name to quickly fill its configuration into the left form.


|**Operation type** |**Template name** |**Decscription** |
|---|---|---|
|SELECT |Enable read access for all users |Allow all users to read table data through select operations. |
|INSERT |Enable insert for authenticated users only |Only logged\-in users are allowed to insert data. |
|DELETE |Enable delete for users based on user_id |Allow users to delete rows where the user_id column matches their ID. |
|INSERT |Enable insert for users based on user_id |Allow users to insert rows where the user_id column matches their ID. |
|UPDATE |Policy with table joins |Use cross\-table queries to build more complex RLS rules suitable for related table scenarios. |
|ALL |Policy with security definer functions |Use security definer functions to implement access control for link tables in many\-to\-many relationships. |
|SELECT |Policy to implement Time To Live (TTL) |Only allow querying rows created within 24 hours to achieve a TTL effect. |
|SELECT |Enable users to view their own data only |Restrict users to query only their own data. |


<span id="srLzVnnV"></span>
### View RLS status

On the **Authentication \> Policies** page, you can view the RLS status of all tables under the current schema:


* **RLS Disabled**: the table has RLS disabled, allowing all users with table\-level permissions to access all data.

* **Enabled**: RLS is enabled for the table, and data access is controlled by policies. If no policies have been created, a warning will appear on the page indicating that data cannot be queried via the API.


You can also switch between different schemas using the schema dropdown menu at the top of the page or use the search box to quickly filter tables and policies.

<span id="t3XW0uUy"></span>
### Disable RLS

To disable RLS for a table, locate the table on the Policies page and click **Disable RLS**. After disabling, data access for the table will no longer be restricted by row\-level policies.

<span id="RdGhNJFh"></span>
## Precautions


* **Default deny**: after enabling RLS, queries on the table through Supabase API (using anon key or user JWT) without creating any policy will return an empty array. Create policies promptly after enabling RLS.

* **service_role unrestricted**: requests initiated with the service_role key bypass RLS and have full database access. Do not expose the service_role key to frontend code or browser environments.

* **Policies and table permissions**: RLS policies take effect on top of table\-level GRANT permissions. Even if a user has table\-level SELECT permission, data cannot be queried without matching RLS policies.

* **Multi\-table queries**: when executing queries with JOINs, each RLS\-enabled table involved applies its own policies independently.

* **Risks of disabling RLS**: after disabling RLS, all users with table\-level permissions can access all data in the table; handle with caution.
