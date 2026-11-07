---
title: "Introduction to Enterprise Knowledge Engine OpenAPI"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Enterprise_Knowledge_Engine_OpenAPI"
---

This article provides a list of OpenAPIs for enterprise knowledge engines, as well as explanations of API\-related terminology, access processes, authentication verification processes, and error handling.

# API List

|Function module |API |Description |
|---|---|---|
|Knowledge Base |[Create Knowledge Bases](https://docs.byteplus.com/docs/dataagent/create-knowledge-bases) |Create a new knowledge base. |
||[Update Knowledge Base](https://docs.byteplus.com/docs/dataagent/update-knowledge-base) |Update knowledge base information, including descriptions, scheduling information, etc. |
||[Knowledge Base Details](https://docs.byteplus.com/docs/dataagent/knowledge-base-details) |Gets knowledge base details, including ID, operation time, description, type, creator, and scheduling configuration. |
||[Get a List of Knowledge Bases](https://docs.byteplus.com/docs/dataagent/get-a-list-of-knowledge-bases) |Get a list of knowledge bases, including the ID, operation time, description, type, creator, and scheduling configuration of each knowledge base. |
||[Delete Knowledge Base](https://docs.byteplus.com/docs/dataagent/delete-knowledge-base) |Deletes the specified knowledge base. |
|Document Management |[Create Document](https://docs.byteplus.com/docs/dataagent/create-document) |Creates a new document in the specified knowledge base. |
||[Query Document](https://docs.byteplus.com/docs/dataagent/query-document) |Query specifies the list of documents in the knowledge base by page. |
||[Document Recall](https://docs.byteplus.com/docs/dataagent/document-recall) |The semantic recall of documents in the specified knowledge base (or doc_ids) is based on the question, and the document meta\-information (overview/guide) is used as the vector source to support multiple channel concurrent recall and fusion, similarity threshold filtering, top_n truncation, and return doc_id list and score. |
||[Get Document Information in Bulk](https://docs.byteplus.com/docs/dataagent/get-document-information-in-bulk) |Get detailed information of documents in the knowledge base in bulk. |
||[Batch Deletion of Documents](https://docs.byteplus.com/docs/dataagent/batch-deletion-of-documents) |Bulk deletes documents and their associated Chunk data based on document IDs. |
||[Delete Document](https://docs.byteplus.com/docs/dataagent/delete-document) |Deletes the specified document and its associated Chunk data based on the document ID. |
||[Start Parsing the Document](https://docs.byteplus.com/docs/dataagent/start-parsing-the-document) |Triggers document parsing to formally perform tasks that divide document content into chunks and index them so they can be retrieved. |
||[Add Document Version](https://docs.byteplus.com/docs/dataagent/add-document-version) |Submit the uploaded individual file as a new version of the target document. |
||[Query Document Version Settings](https://docs.byteplus.com/docs/dataagent/query-document-version-settings) |Query version write policy and version number rules. |
||[Update Document Version Settings](https://docs.byteplus.com/docs/dataagent/update-document-version-settings) |Uniformly update version writing policies and version number rules; rule changes recalculate historical display version numbers. |
||[Query Document Version List](https://docs.byteplus.com/docs/dataagent/query-document-version-list) |Query the full version of the document and its current active status. |
||[Switch Document Version](https://docs.byteplus.com/docs/dataagent/switch-document-version) |Switch the active version in real time and disable the old version after the switch. |
||[Delete Document Version](https://docs.byteplus.com/docs/dataagent/delete-document-version) |Delete non\-active and non\-working document versions. |
||[Get Document](https://docs.byteplus.com/docs/dataagent/get-document) |Get the document content in the knowledge base (such as downloading files) through the document ID. |
||[Edit Document Configuration](https://docs.byteplus.com/docs/dataagent/edit-document-configuration) |Edit the specific document parsing configuration in the knowledge base and submit subsequent execution tasks. After calling the current interface, the relevant task is only submitted and has not been officially executed, and must continue to be called [Start Parsing the Document](https://docs.byteplus.com/docs/dataagent/start-parsing-the-document) before it will actually start execution. |
||[Create Folder](https://docs.byteplus.com/docs/dataagent/create-folder) |Create a new folder by specifying the parent folder ID and folder type. |
||[Query Folder List](https://docs.byteplus.com/docs/dataagent/query-folder-list) |Gets a list of all folders under the specified knowledge base and returns it in a tree structure. |
||[Query the Knowledge Base Directory File Tree](https://docs.byteplus.com/docs/dataagent/query-the-knowledge-base-directory-file-tree) |Get the current user visible knowledge base directory and file tree, support name keyword filtering. |
||[Move Documents or Folders](https://docs.byteplus.com/docs/dataagent/move-documents-or-folders) |Moves the specified document or folder to the target parent folder. Before invoking the current interface, you can call [Query Folder List](https://docs.byteplus.com/docs/dataagent/query-folder-list) to get optional destination folder. |
||[Update Folder Name](https://docs.byteplus.com/docs/dataagent/update-folder-name) |Updates the name of the specified folder. |
||[Delete Folder](https://docs.byteplus.com/docs/dataagent/delete-folder) |Delete the specified folder. |
||[Get Document Version Content](https://docs.byteplus.com/docs/dataagent/get-document-version-content) |Reads the Markdown content of the specified version of the document accessible to the current tenant, doc_id and version_id. |
||[Enable or Disable Documents in Bulk](https://docs.byteplus.com/docs/dataagent/enable-or-disable-documents-in-bulk) |Enable or disable documents in bulk, and also support enabling or disabling chunks under a specified document. Before calling the current interface, you can first call [Query Document](https://docs.byteplus.com/docs/dataagent/query-document) to obtain the document to be operated. |
|File Management |[Upload File](https://docs.byteplus.com/docs/dataagent/upload-file) |Upload files to the knowledge base system, support multiple file formats, and return file meta information. After calling the current interface, the file has not yet started parsing, and must continue to call [File Associate with Knowledge Base](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base) to complete the file association knowledge base and parsing parameter configuration. |
|Segment Management |[Get Chunk List](https://docs.byteplus.com/docs/dataagent/get-chunk-list) |Get a list of chunks by knowledge base or document, supporting keywords, available status, and sorting criteria. The returned result contains metadata such as Chunk's basic content, enabling status, and additional information. |
||[Modify Chunk](https://docs.byteplus.com/docs/dataagent/modify-chunk) |Modify the Chunk content of the file in the specified knowledge base to support updating text, metadata and other information. |
||[Knowledge Base Retrieval](https://docs.byteplus.com/docs/dataagent/knowledge-base-retrieval) |Retrieve relevant document fragments in the knowledge base based on semantics or keywords, and support knowledge meta\-information filtering. Requests can be filtered by label_value_ids, label_values, enable_filters, and extra control tags, permissions, expiration time, and extended meta information; responses return Chunk similarity meta information such as knowledge display name, comprehensive similarity, vector similarity, keyword similarity, and rearrangement classification. |
||[Multi-Knowledge Base Retrieval](https://docs.byteplus.com/docs/dataagent/multi-knowledge-base-retrieval) |Parallel retrieval of multiple knowledge bases based on semantics or keywords, and fusing to return relevant document fragments. The interface follows the knowledge base, documents, tags, permissions, and expiration filter rules. |
||[Batch Import of QA Knowledge](https://docs.byteplus.com/docs/dataagent/batch-import-of-qa-knowledge) |Bulk import QA library, Query library, or terminology library knowledge through uploaded table files. |
||[Batch Export of QA Knowledge](https://docs.byteplus.com/docs/dataagent/batch-export-of-qa-knowledge) |Batch export of knowledge items in QA library, Query library or terminology library, support exact export by item ID or export all matching content by query condition. The interface returns the asynchronous export task ID, and the task results can be viewed later in the download task list. |
||[Query Knowledge Import Task of QA Type](https://docs.byteplus.com/docs/dataagent/query-knowledge-import-task-of-qa-type) |Query import in batch task progress of QA library, Query library or term library by page. Return task status, number of successes, number of failures and failed file download address. Typically, after calling [Batch Import of QA Knowledge](https://docs.byteplus.com/docs/dataagent/batch-import-of-qa-knowledge), the import results are tracked using the current interface. |
|File to Document |[File Associate with Knowledge Base](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base) |Associates uploaded files to the specified knowledge base and configures parsing parameters. Before calling the current interface, it should call [Upload File](https://docs.byteplus.com/docs/dataagent/upload-file) first; after completing the current interface, the relevant tasks are only submitted, not yet officially executed, and must continue to call [Start Parsing the Document](https://docs.byteplus.com/docs/dataagent/start-parsing-the-document) before they really start to execute. |
||[Read Table Header](https://docs.byteplus.com/docs/dataagent/read-table-header) |Read the header information of the uploaded table file for subsequent data mapping configuration |
|Query and Graph Retrieval |[Graph Retrieval](https://docs.byteplus.com/docs/dataagent/graph-retrieval) |Performs a vector + graph hybrid search on the specified graph to return the recall content without going through the large model. |
|Session Management |[Create a Session](https://docs.byteplus.com/docs/dataagent/create-a-session) |Create a new conversation session to record the interaction history between the user and the AI application. |
||[Fetch Session List](https://docs.byteplus.com/docs/dataagent/fetch-session-list) |Query all session records under the specified conversation by page, supporting filtering by source type. |
||[Fetch Chat Content in Session](https://docs.byteplus.com/docs/dataagent/fetch-chat-content-in-session) |Get the history of chat messages in the specified session by page, in chronological order. |
||[Retrieval Application Call](https://docs.byteplus.com/docs/dataagent/retrieval-application-call) |Invokes the published retrieval application, returning a pure recall result. |
||[V4 Smart Q&A](https://docs.byteplus.com/docs/dataagent/v4-smart-q-a) |Initiate V4 intelligent Q&A, support enterprise knowledge, personal knowledge, ontology semantics, Knowledge Graph, attachments, networked search, and deep thinking, and return results in SSE streaming. |
||[V4 Smart Q&A Attachment Upload](https://docs.byteplus.com/docs/dataagent/v4-smart-q-a-attachment-upload) |Upload the temporary analysis attachment used by V4 Intelligent Q&A, and return the attachment information that can be referenced in the Q&A message. |
||[V4 Session Creation or Renaming](https://docs.byteplus.com/docs/dataagent/v4-session-creation-or-renaming) |Create a V4 Q&A session, or rename an existing session based on the session ID. |
||[V4 Session List](https://docs.byteplus.com/docs/dataagent/v4-session-list) |Pull the current user's V4 intelligent Q&A session by page, supports keyword filtering, and keeps source compatibility parameters. |
||[V4 Session Message List](https://docs.byteplus.com/docs/dataagent/v4-session-message-list) |Pull the chat history and final results in the specified V4 Q&A session by page. |
|Document Permission Management |[Query Tag List](https://docs.byteplus.com/docs/dataagent/query-label-list) |Query the list of labels under the current tenant by page, with support for keywords, knowledge base, and automatic label filtering. |
||[New Label](https://docs.byteplus.com/docs/dataagent/new-label) |Create a new document/knowledge base tag. |
||[Bind or Create a Label](https://docs.byteplus.com/docs/dataagent/bind-or-create-a-label) |Bind a tag for a specified document; when the tag value does not exist, you can create a tag value and bind it according to the requested content. You can call [New Label](https://docs.byteplus.com/docs/dataagent/new-label) first to create labels, or you can call [Label the Document](https://docs.byteplus.com/docs/dataagent/label-the-document) to execute only existing label bindings. |
||[Label the Document](https://docs.byteplus.com/docs/dataagent/label-the-document) |Adds a label to the specified document. |
||[Label Documents in Batches](https://docs.byteplus.com/docs/dataagent/label-documents-in-batches) |Bind tags to multiple documents in batches and return the processing results for each document. The call should be made by [New Label](https://docs.byteplus.com/docs/dataagent/new-label) to create a label. |
||[Remove Document Labels](https://docs.byteplus.com/docs/dataagent/remove-document-labels) |Removes a tag from the specified document or knowledge base. |
||[Remove the Specified Document Label](https://docs.byteplus.com/docs/dataagent/remove-the-specified-document-label) |Removes the specified label value from the specified document. The caller requires tenant administrator privileges. |
||[Delete Label](https://docs.byteplus.com/docs/dataagent/delete-label) |Deletes the specified label. |
||[Set Document Valid Period](https://docs.byteplus.com/docs/dataagent/set-document-valid-period) |Sets the valid period for individual documents and optionally deletes them automatically when they expire. |
||[Batch Configuring Document Valid Period](https://docs.byteplus.com/docs/dataagent/batch-configuring-document-valid-period) |Set the valid period of multiple documents in batches, and choose to delete them automatically after expiration. |
||[Get Document Label](https://docs.byteplus.com/docs/dataagent/get-document-label) |Sets the valid period for individual documents and optionally deletes them automatically when they expire. |
||[Get the QA Label](https://docs.byteplus.com/docs/dataagent/get-the-qa-label) |Query the label of a single QA from sophon qa_id and map the label_id/label_value_id returned by sophon back to the label_name/value of verag. Only for QA system (QA/Cache/Term) libraries. |
||[Download QA Label CSV](https://docs.byteplus.com/docs/dataagent/download-qa-label-csv) |Export all labels and their values under the current tenant, one label per row. The tag column gives the same string as the QA Excel import tag field (such as'City: Shanghai, Beijing '), and label_type columns are marked with single/multiple selections. Returns the UTF\-8 (BOM) encoded CSV. Requires that the current user has read access to the knowledge base module (consistent with kb/list). |
||[Get Label Details by Label ID](https://docs.byteplus.com/docs/dataagent/get-label-details-by-label-id) |Gets tag details and a list of values by tag ID. |
||[Get Label Details by Label Name](https://docs.byteplus.com/docs/dataagent/get-label-details-by-label-name) |Gets label details and a list of values by label name. The caller requires tenant administrator privileges. |
|Hybrid Retrieval |[Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) |Query the table structure of the underlying search engine, returning primary keys, field definitions, vector fields, and full\-text search field configurations. |
||[Append Hybrid Retrieval Field](https://docs.byteplus.com/docs/dataagent/append-hybrid-retrieval-field) |Append fields to the table of existing underlying search engines, and declare vector search fields and full\-text search fields synchronously. Before calling, query the current table structure by [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) for . |
||[Delete Hybrid Retrieval Field](https://docs.byteplus.com/docs/dataagent/delete-hybrid-retrieval-field) |Delete a single field from the table of the underlying search engine. Before calling, you should confirm that the target table and fields exist, and you can call [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) first to view the current table structure. |
||[Bulk Removal of Hybrid Retrieval Fields](https://docs.byteplus.com/docs/dataagent/bulk-removal-of-hybrid-retrieval-fields) |Bulk deletes multiple fields from the underlying search engine's table. Before calling, you should confirm that the target table and fields exist, and you can call [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) first to view the current table structure. |
||[Delete Data by Filter](https://docs.byteplus.com/docs/dataagent/delete-data-by-filter) |Delete the data in the tables of the underlying search engine by DSL filtering. Before calling, you can use [Hybrid Recall](https://docs.byteplus.com/docs/dataagent/hybrid-recall) to verify that the filter conditions can accurately hit the data to be deleted to avoid accidental deletion. |
||[Create Table Structure](https://docs.byteplus.com/docs/dataagent/create-table-structure) |Create a table structure for the underlying search engine, declaring field definitions, vector search fields, and full\-text search fields. Before writing data, you should call the current interface to complete the table construction, and then call the [Write Data](https://docs.byteplus.com/docs/dataagent/write-data) to write data. |
||[Write Data](https://docs.byteplus.com/docs/dataagent/write-data) |Write data to the table of the underlying search engine. Before calling the current interface, you should first call [Create Table Structure](https://docs.byteplus.com/docs/undefined/6ad751ccc7ae8502f66604d1) to create table structure, or confirm that the target table already exists; after writing, you can call [Hybrid Recall](https://docs.byteplus.com/docs/undefined/6ad751e2349c6002d8c367aa) to verify the recall effect. |
||[Delete Data](https://docs.byteplus.com/docs/dataagent/delete-data) |Delete data from the underlying search engine's table by data ID. Before calling, you can call [Create Table Structure](https://docs.byteplus.com/docs/dataagent/create-table-structure) to confirm that the target table exists, and confirm that the ID comes from the data that has been written by [Write Data](https://docs.byteplus.com/docs/dataagent/write-data). |
||[Hybrid Recall](https://docs.byteplus.com/docs/dataagent/hybrid-recall) |Execute a hybrid recall query against the underlying search engine's table based on DSL. Before calling the current interface, you should first call [Create Table Structure](https://docs.byteplus.com/docs/dataagent/create-table-structure) to complete table structure creation, and call [Write Data](https://docs.byteplus.com/docs/dataagent/write-data) to write data that can be recalled. |
|Version management |[Enable Version Management](https://docs.byteplus.com/docs/dataagent/enable-version-management) |Create a version group for the specified document and enable version management. |
||[New Version Type](https://docs.byteplus.com/docs/dataagent/new-version-type) |Sets the version type for the specified version group. |
||[Get Version List](https://docs.byteplus.com/docs/dataagent/get-version-list) |Gets the version list and details for the specified version group. |
|System Permission Management |[Add Tenant Users in Bulk](https://docs.byteplus.com/docs/dataagent/add-tenant-users-in-bulk) |Add users to the current tenant in bulk. |
||[Remove Users from Tenants](https://docs.byteplus.com/docs/dataagent/remove-users-from-tenants) |Batch removal of users from the current tenant. The caller requires administrative privileges and cannot remove the administrative user. |
||[Update User Status](https://docs.byteplus.com/docs/dataagent/update-user-status) |Enable or disable the tenant user. The caller requires administrator or owner privileges and is subject to administrator, owner, and personal action restrictions. |
||[Module Authorization in Bulk/Cancel Module Permissions](https://docs.byteplus.com/docs/dataagent/module-authorization-in-bulk-cancel-module-permissions) |Batch authorization/revocation of module permissions (supports users, roles, departments). |
||[Batch Query Current User Resource Permissions](https://docs.byteplus.com/docs/dataagent/batch-query-current-user-resource-permissions) |Query the valid resource permissions of the current authenticated user in batches by value resource_id, without querying the upstream resource directory. |
||[Query Current User Authorization Resource ID Range](https://docs.byteplus.com/docs/dataagent/query-current-user-authorization-resource-id-range) |Query the numeric resource_id accessible to the current authenticated user by resource type and action; the tenant administrator returns unrestricted = true. |
||[Resource Permission Authorization/Cancel Authorization](https://docs.byteplus.com/docs/dataagent/resource-permission-authorization-cancel-authorization) |Resource permission authorization/de\-authorization. |
|Personal Wiki Workspace Content |[Acquire Original Personal Knowledge Base File](https://docs.byteplus.com/docs/dataagent/acquire-original-personal-knowledge-base-file) |Get the original download address of the current user's personal knowledge base document; the Lark document returns the Lark original address. |
||[Acquire Personal Knowledge Base Markdown](https://docs.byteplus.com/docs/dataagent/acquire-personal-knowledge-base-markdown) |Gets the readable Markdown address of the current user's personal knowledge base document; returns an empty address when the product is not ready. |
||[Personal Knowledge Base Search](https://docs.byteplus.com/docs/dataagent/personal-knowledge-base-search) |Recall relevant chunks in the personal knowledge base of the user bound to the current application token; support qualified documentation and recall parameters. |
|Personal Wiki Workspace Documentation |[Get the List of Personal Knowledge Base Documents](https://docs.byteplus.com/docs/dataagent/get-the-list-of-personal-knowledge-base-documents) |Query current application Token binding user imported personal knowledge base documents by page, the result does not contain folders. |
|Personal Wiki Workspace Import |[Import Personal Knowledge Base Documents](https://docs.byteplus.com/docs/dataagent/import-personal-knowledge-base-documents) |Upload the file to the personal knowledge base of the user bound to the current application Token, and submit the parsing task using the server level fixed parsing configuration. |
|Personal Wiki Workspace Resources |[Get the Sublist of Personal Knowledge Base Resources](https://docs.byteplus.com/docs/dataagent/get-the-sublist-of-personal-knowledge-base-resources) |Query Token bound to the user's personal knowledge base resource sub\-list by page: the root layer returns the knowledge base list, after specifying the parent resource returns the same level folders and documents. |
|Structured Knowledge Base Import |[Upload Structured File](https://docs.byteplus.com/docs/dataagent/upload-structured-file) |Upload a CSV or Excel file and return the file_id used for subsequent asset creation and import. |
||[Initiate Structured Data Import](https://docs.byteplus.com/docs/dataagent/initiate-structured-data-import) |After automatically ensuring that OpenSearch indexing is ready, initiate a local file or Prep dataset import and return a unified task reference. |
||[Query Structured Task](https://docs.byteplus.com/docs/dataagent/query-structured-task) |Use unified task_ref to query local file imports, Prep dataset imports, or asynchronous deletion task status. |
||[Create Structured Data Assets](https://docs.byteplus.com/docs/dataagent/create-structured-data-assets) |Create CSV, Excel, ClickHouse or Hive data assets and field drafts. |
|Structured Knowledge Base Management |[Create a Structured Knowledge Base](https://docs.byteplus.com/docs/dataagent/create-a-structured-knowledge-base) |Create a structured knowledge base and register creator permissions for the current caller. |
||[Query the List of Structured Knowledge Bases](https://docs.byteplus.com/docs/dataagent/query-the-list-of-structured-knowledge-bases) |Pages by name, keyword, and status to query the structured knowledge base that the current caller has access to. |
||[Query the Structured Knowledge Base Directory](https://docs.byteplus.com/docs/dataagent/query-the-structured-knowledge-base-directory) |Query the structured knowledge base directory tree and return the root directory and its subdirectories with the same name as the knowledge base. |
||[Query the List of Structured Data Assets](https://docs.byteplus.com/docs/dataagent/query-the-list-of-structured-data-assets) |Query structured data assets based on directory, data source, processing status, or keywords of name by page. |
||[Query Structured Data Asset Details](https://docs.byteplus.com/docs/dataagent/query-structured-data-asset-details) |Queries public metadata such as the source, status, file size, number of rows, and recent error of the specified data asset. |
||[Delete Structured Data Assets](https://docs.byteplus.com/docs/dataagent/delete-structured-data-assets) |Delete the data asset and its OpenSearch index; the same request can be safely retried. |
||[Delete the Structured Knowledge Base](https://docs.byteplus.com/docs/dataagent/delete-the-structured-knowledge-base) |Asynchronously removes the knowledge base and all its data assets and indexes, and returns the task reference. |
|Structured Knowledge Base Query |[Query Structured Data Rows](https://docs.byteplus.com/docs/dataagent/query-structured-data-rows) |Query structured data rows by keyword, sort, and paging criteria. |
||[Query Structured Row Details](https://docs.byteplus.com/docs/dataagent/query-structured-row-details) |Query individual pieces of structured data based on stable row_key. |
||[Add a Structured Data Row](https://docs.byteplus.com/docs/dataagent/add-a-structured-data-row) |Add a new row of data to the structured data asset that is ready. |
||[Edit Structured Data Rows](https://docs.byteplus.com/docs/dataagent/edit-structured-data-rows) |A row of data is partially updated according to the stable row_key, and the unpassed field remains the original value. |
||[Delete Structured Data Rows](https://docs.byteplus.com/docs/dataagent/delete-structured-data-rows) |Deletes a row of data according to the stable row_key; returns idempotently when the target row no longer exists. |
||[Update Structured Data Table Structure](https://docs.byteplus.com/docs/undefined/6ad8231ea37afb02a5334fc7) |Add fields or edit enable, filter, return, vector, display name, and description configurations; physical field deletion, field renaming, and data type modification are not supported. |
||[Query Structured Data Table Structure](https://docs.byteplus.com/docs/dataagent/query-structured-data-table-structure) |Query logical fields, filter/vector/return capabilities, and OpenSearch index\-ready status without exposing underlying mappings. |
||[Query Field Enumeration Value Sample](https://docs.byteplus.com/docs/dataagent/query-field-enumeration-value-sample) |Query the enumeration sample and occurrences of the specified logical field for filter value selection. |
||[Recall Structured Knowledge](https://docs.byteplus.com/docs/dataagent/recall-structured-knowledge) |Performs a mixed search by single table scope, exact filtering, semantic fields, return fields, and sort parameters and returns rows of data. |
|Account Center |[Batch New Users](https://docs.byteplus.com/docs/dataagent/batch-new-users) |Create new user accounts in batches, support email, mobile phone number, status and custom attributes. |

# Explanation of terms

|**Field Chinese** |**Field English** |**Description** |
|---|---|---|
|Group |X\-Org |A main account opened for you on the SaaS environment is a group, and the groups are completely independent of each other's data, functions, and users. Private deployment environment, such as the opening of multi\-group, an environment supports multiple groups, and the data between different groups is completely isolated; if multi\-group is not opened, a set of environments is a group. |
|Project |X\-Tenant |Under a group, multiple projects can be created, and under a group, users can limit the projects that can be accessed through permission settings. Projects are required fields when API calls are made. |
|Application |\-\- |The basic unit of the calling API. When calling the API, you need to log in to the Enterprise Knowledge Engine console, create an application in Open API \> Application Management Function, and obtain the AccessKey. |

# Access process

VeRAG application authentication is a token\-based API access authentication mechanism. The user creates an application through the web interface and obtains a unique token (AK), which is then used to invoke the authorized business API interface.

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1ODVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTg1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNDIgMzIgTCAyMTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMjAuODggMzIgTCAyMTMuODggMzUuNSBMIDIxNS42MyAzMiBMIDIxMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5XZWIgcGFnZSBjcmVhdGVzIGFwcGxpY2F0aW9uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM2MiAzMiBMIDQzNS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ0MC44OCAzMiBMIDQzMy44OCAzNS41IEwgNDM1LjYzIDMyIEwgNDMzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMjIiIHk9IjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5HZXQgVG9rZW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ0MiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlVzZSBUb2tlbiB0byBjYWxsIGJ1c2luZXNzIEFQSTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

## Step 1: Create an app and obtain tokens

1. Log in to the Marketing Agent platform.

2. Enter Enterprise Knowledge Engine in the left navigation bar.

3. In the left navigation bar of the Enterprise Knowledge Engine, select **Project Center** \> **open API** \> **Application Management**.

4. In the upper right corner of the **app management** page, click **New app**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39fba30778e04108a8596d26dacefe4a~tplv-goo7wpa0wc-image.image)

5. On the New App page, complete the following configuration and click **Save**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a69947e84744060816e4585b118aa78~tplv-goo7wpa0wc-image.image)

   |**Module** |**Configuration item** |**Description** |
   |---|---|---|
   |Basic information |App name |A custom name that identifies the current application. |
   ||APIs available for application use |Select the OpenAPI scope of the enterprise knowledge engine that can be invoked by the current application. |
   |Call OpenAPI authentication method |Access to Authorizable Items |Specifies the items that the current app can authorize. |
   ||Associated user |Specify the user identity when accessing the API. |

6. (Optional) The created app can be viewed in the app list, where you can select the following actions.

   * In the list, you can view the basic information of the application, including the name, associated API, associated user, and other information.

   * In the upper right corner of the page, it is supported to switch the viewing method of the application(**table** or **card**).

   * In the **operation** column, click **Edit** to modify the configuration information of the current application.

   * Click **Delete** in the **operation** column to delete apps that are no longer needed.

      > **注意**

      > Once the application is deleted, it cannot be restored, please operate with caution.

7. In the application list, get the application token.

   Subsequent calls to OpenAPI require passing in the token of the application being used.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c09b63151d354680998dad2b7083996f~tplv-goo7wpa0wc-image.image)

   **Token information description:**

   |**Field** |**Description** |
   |---|---|
   |Token (AK) |Access key for API authentication |
   |Authorized Tenant (tenant_ids) |List of tenant/project IDs accessible by Token |
   |Authorization API (api_paths) |List of API paths accessible by Token |

## Step 2: Use Token to invoke the API

You can refer to the following parameter descriptions and call examples to learn how to use Token to call the API.

### Authentication Header Configuration

When calling the business API, you need to add the following information to the request header:

|**Header** |**Value format** |**Description** |
|---|---|---|
|Authorization |`Bearer <token>` |Authentication Token, format is Bearer + Space + Token |
|X\-Org |`<org_id>` |Organization ID |
|X\-Tenant |`<tenant_id>` |Tenant/Project ID (must be in authorized tenant_ids list) |
|X\-User\-Id |`<user_id>` |Required conditions. When applying user mode to "specify user on request", it can be used to specify the downstream user of this call, with priority higher than X\-User; the system will verify that the user belongs to the current X\-Org and X\-Tenant and the status is valid |
|X\-User |`<user_account>` |Required conditions. When applying user mode to "specify user on request", it can be used to specify the downstream user for this call; if X\-User\-Id is passed in at the same time, X\-User\-Id shall prevail. "Associate a specified user" mode does not need to be passed in, and the incoming is ignored |

### HTTP request example

```HTTP
GET {base_url}/marketing_agent/api/v2/open_application/openapi/{product}/{api_path}
Authorization: Bearer a1b2c3d4e5f6g7h8xxxx
X-Org: 1
X-Tenant: 1
```

* `{base_url}`: API request URL, fixed to `https://console.volcengine.com`for SaaS environment.

* `{Product}`: Product name, such as Enterprise Knowledge Engine for `VeRAG`.

* `{api_path}`: The interface path can be obtained through the corresponding API document, such as the interface path of "Query Document" is `/document/list`.

### Python example

```Python
import requests

#configuration
BASE_URL = "https://your-api-domain.com"
TOKEN = "{your_token}"
ORG_ID = 1
TENANT_ID = 1

Product and interface configuration
product = "VeRAG"  Product names such as Enterprise Knowledge Engine for VeRAG
endpoint = "{api_path}"  #Interface path, which can be obtained through the corresponding API documentation

#request header
headers = {
    "Authorization": f"Bearer {TOKEN}",
    "X-Org": str(ORG_ID),
    "X-Tenant": str(TENANT_ID),
    "Content-Type": "application/json"
}

#Send a request
response = requests.get(
    f"{BASE_URL}/marketing_agent/api/v2/open_application/openapi/{product}/{api_path}",
    headers=headers
)

print(response.json())
```

### cURL example

```Bash
curl -X GET "https://your-api-domain.com/marketing_agent/api/v2/open_application/openapi/{product}/{api_path}" \
  -H "Authorization: Bearer {your_token}" \
  -H "X-Org: 1" \
  -H "X-Tenant: 1" \
  -H "Content-Type: application/json"
```

Taking the [Query Document](https://docs.byteplus.com/docs/dataagent/query-document) interface as an example, the cURL call example is as follows:

```Bash
curl --location 'https://your-api-domain.com/marketing_agent/api/v2/open_application/openapi/VeRAG/document/list?kb_id=89&page=1&page_size=10' \
--header 'X-Org: 1' \
--header 'X-Tenant: 1' \
--header 'Authorization: Bearer {your_token}'
```

# Authentication verification process

When calling the API with Token, the system performs the following verification:

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NDVweCIgaGVpZ2h0PSI1NjVweCIgdmlld0JveD0iLTAuNSAtMC41IDQ0NSA1NjUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIyMiA2MiBMIDIyMiA5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIyMiAxMDAuODggTCAyMTguNSA5My44OCBMIDIyMiA5NS42MyBMIDIyNS41IDkzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA0MzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iY29sb3I6cmdiKDUxLCA1MSwgNTEpO2ZvbnQtZmFtaWx5Om1vbm9zcGFjZSwgbW9ub3NwYWNlO2ZvbnQtc2l6ZToxNHB4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ4LCAyNDgpIj4xLiBDaGVjayB3aGV0aGVyIDxiPkF1dGhvcml6YXRpb24gSGVhZGVyPC9iPiBleGlzdHM8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIyMiAxNjIgTCAyMjIgMTk1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIyIDIwMC44OCBMIDIxOC41IDE5My44OCBMIDIyMiAxOTUuNjMgTCAyMjUuNSAxOTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIxMDIiIHdpZHRoPSI0NDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJjb2xvcjpyZ2IoNTEsIDUxLCA1MSk7Zm9udC1mYW1pbHk6bW9ub3NwYWNlLCBtb25vc3BhY2U7Zm9udC1zaXplOjE0cHg7dGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OCwgMjQ4KSI+Mi4gVmVyaWZ5IGZvcm1hdCBpcyAiPGI+QmVhcmVyICZsdDt0b2tlbiZndDs8L2I+IiBvciBub3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIyMiAyNjIgTCAyMjIgMjk1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIyIDMwMC44OCBMIDIxOC41IDI5My44OCBMIDIyMiAyOTUuNjMgTCAyMjUuNSAyOTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyMDIiIHdpZHRoPSI0NDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJjb2xvcjpyZ2IoNTEsIDUxLCA1MSk7Zm9udC1mYW1pbHk6bW9ub3NwYWNlLCBtb25vc3BhY2U7Zm9udC1zaXplOjE0cHg7dGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OCwgMjQ4KSI+My4gPC9zcGFuPjxmb250IGNvbG9yPSIjMzMzMzMzIiBmYWNlPSJtb25vc3BhY2UsIG1vbm9zcGFjZSI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNHB4Ij5TZWFyY2ggZm9yIHRoZSBjb3JyZXNwb25kaW5nIGFwcGxpY2F0aW9uIGNvbmZpZ3VyYXRpb24gYmFzZWQgb24gdGhlwqA8L3NwYW4+PC9mb250PjxzcGFuIHN0eWxlPSJmb250LXdlaWdodDpib2xkZXI7Y29sb3I6cmdiKDUxLCA1MSwgNTEpO2ZvbnQtZmFtaWx5Om1vbm9zcGFjZSwgbW9ub3NwYWNlO2ZvbnQtc2l6ZToxNHB4O3RleHQtYWxpZ246c3RhcnQiPlRva2VuPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyMjIgMzYyIEwgMjIyIDM5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIyMiA0MDAuODggTCAyMTguNSAzOTMuODggTCAyMjIgMzk1LjYzIEwgMjI1LjUgMzkzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMzAyIiB3aWR0aD0iNDQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0idGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OCwgMjQ4KTtmb250LXNpemU6MTRweDtmb250LWZhbWlseTptb25vc3BhY2UsIG1vbm9zcGFjZTtjb2xvcjpyZ2IoNTEsIDUxLCA1MSkiPjQuwqA8L3NwYW4+PHNwYW4gc3R5bGU9ImNvbG9yOnJnYig1MSwgNTEsIDUxKTtmb250LWZhbWlseTptb25vc3BhY2UsIG1vbm9zcGFjZTtmb250LXNpemU6MTRweDt0ZXh0LWFsaWduOnN0YXJ0O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ4LCAyNDgpIj5WZXJpZnkgd2hldGhlcjwvc3Bhbj48c3BhbiBzdHlsZT0idGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OCwgMjQ4KTtmb250LXNpemU6MTRweDtmb250LWZhbWlseTptb25vc3BhY2UsIG1vbm9zcGFjZTtjb2xvcjpyZ2IoNTEsIDUxLCA1MSkiPsKgPGI+WC1UZW5hbnQ8L2I+wqBpcyBpbiB0aGUgYXV0aG9yaXplZMKgPGI+dGVuYW50X2lkczwvYj7CoGxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIyMiA0NjIgTCAyMjIgNDk1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIyIDUwMC44OCBMIDIxOC41IDQ5My44OCBMIDIyMiA0OTUuNjMgTCAyMjUuNSA0OTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI0MDIiIHdpZHRoPSI0NDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJjb2xvcjpyZ2IoNTEsIDUxLCA1MSk7Zm9udC1mYW1pbHk6bW9ub3NwYWNlLCBtb25vc3BhY2U7Zm9udC1zaXplOjE0cHg7dGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OCwgMjQ4KSI+NS4gVmVyaWZ5IHJlcXVlc3RlZMKgPGI+QVBJPC9iPsKgcGF0aCBpcyBpbiB0aGUgYXV0aG9yaXplZMKgPGI+YXBpX3BhdGhzPC9iPsKgbGlzdDwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjUwMiIgd2lkdGg9IjQ0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA0MzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1MzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImNvbG9yOnJnYig1MSwgNTEsIDUxKTtmb250LWZhbWlseTptb25vc3BhY2UsIG1vbm9zcGFjZTtmb250LXNpemU6MTRweDt0ZXh0LWFsaWduOnN0YXJ0O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ4LCAyNDgpIj42LsKgPC9zcGFuPjxmb250IGNvbG9yPSIjMzMzMzMzIiBmYWNlPSJtb25vc3BhY2UsIG1vbm9zcGFjZSI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxNHB4Ij5BdXRoZW50aWNhdGlvbiBwYXNzZWQsIGV4ZWN1dGUgcmVxdWVzdDwvc3Bhbj48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+)

# Error handling

Common error messages, causes, and solutions are described as follows:

|**Error message** |**Reason** |**Solution** |
|---|---|---|
|`Authorization missing` |Authorization Header not provided |Add Authorization Header |
|`Please check your authorization format` |Authorization format error |Use the `Bearer < token >`format |
|`Need bearer auth` |Bearer authentication type not used |Using `Bearer`Authentication Types |
|`no found user app about token` |Token is invalid or does not exist |Check if the Token is correct |
|`Please check your org_id and tenant_id` |org_id or tenant_id missing or malformed |Check X\-Og and X\-Tenant Header |
|`no found tenant config about token` |Tenant ID not authorized |Use the tenant_id in the authorization list |
|`the route path is UnAuthorized` |API path is not authorized |Confirm that the API is authorized in the application |

# Safety advice

* **Secure the Token**

   Token is equivalent to password, please do not disclose or submit to public repository.

* **Principle of least privilege**

   Authorize only the necessary API paths and tenant IDs.

* **Regular change**

   It is recommended to regularly delete the old application through the interface and create a new application to update the Token.

* **Use HTTPS**

   Make sure all API calls are made over HTTPS to prevent token theft

* **Recycle in time**

   Apps that are no longer used should be deleted in time to avoid the risk of token leaks.
