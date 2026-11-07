---
title: "Supabase console overview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Supabase_console_overview"
---

You can activate the Supabase service on the BytePlus AI Native Database Platform console. By establishing public or private network connections and configuring API keys according to business scenarios, you can leverage all BaaS services available on the Supabase console.

The Supabase console currently offers the following core function modules:

### **Database**

PostgreSQL is the core component of the Supabase console. Each Supabase project includes a complete PostgreSQL instance by default, supporting native PostgreSQL capabilities and 50+ extensions, along with visual management tools (Table Editor and SQL Editor).

At the database usage level, Supabase supports operating database objects such as databases, tables, functions, and stored procedures through RESTful and GraphQL interfaces. Compared to the traditional development of a separate DAO layer within applications, accessing the database directly via API eliminates the need to implement an additional DAO layer, requiring only the business logic to be written.

* **RESTful interface**: implements based on the PostgREST framework, automatically converting HTTP API requests into SQL and featuring a built\-in connection pool. When handling high concurrency HTTP requests, the number of connections between PostgREST and the database can be kept low, preventing excessive memory usage caused by too many connections to the PostgreSQL database.

* **GraphQL interface**: implements based on the pg_graphql extension, request results are usually returned in formats like JSONB for easy frontend consumption.

### **Authentication (authentication & user management)**

The Auth module offers fine\-grained permission control based on PostgreSQL row\-level security (RLS) and includes a complete user identity system to help developers quickly build secure and reliable user systems.

* **Fine\-grained permission control**: relying on PostgreSQL row\-level security, it implements precise access control based on users, roles, and data conditions. Users can define access rules using SQL. All queries automatically apply security policies to ensure data security and privacy.

* **Secure communication and access control**: achieve secure communication based on JWT, and combine with row\-level security policies to precisely control user access to data.

* **User management capability**: provides complete user management functions including user registration, login, and password management, and allows user information management via APIs to help developers build a comprehensive user identity management system.

* **Authentication method**: supports email login, OAuth third\-party authentication (e.g., WeChat, Google, GitHub, Facebook, Lark), SMS verification and login (including Volcengine SMS service), CAS (Central Authentication Service), ~~and other~~ methods.

### **Storage**

Storage provides an extensible file storage solution that supports storing and accessing various file types including images, videos, and documents. Combined with PostgreSQL's RLS rules, file access can be finely controlled to meet security needs in various scenarios.

### **Edge Function**

Edge Function is built on the Volcengine veFaaS function service and provides a set of serverless function capabilities. Users can write, deploy, and run JavaScript (Deno) or Python code within it, placing complex business logic in Edge Function to achieve secure isolation from the front end and other BaaS services.

Typical applicable scenarios include:

* Handling payment callbacks

* Form validation and data preprocessing

* Third\-party API integration

* Direct AI models access such as large models

Edge Function can directly call other Supabase services without additional key configuration.

### **Realtime (message notification)**

The Supabase console provides real\-time message communication and broadcasting through the Realtime component. The client connects to Realtime via WebSocket. Combined with PostgreSQL database’s built\-in logical replication slot and trigger, and by monitoring changes in Realtime’s messages system table, record updates in the database can be pushed in real time to multiple clients.

In Realtime, multiple Realtime services across different regions can also propagate messages. This feature is crucial for highly interactive scenarios, such as real\-time chat applications or collaboration tools. For example, in a chat application, when user A sends a message, all clients connected to that channel (such as user B's devices) immediately receive the update without polling the server.

Based on Realtime, developers can quickly build collaboration applications. Typical scenarios include:

* **Data synchronization**: achieves data sync among multiple clients based on PostgreSQL’s replication mechanism.

* **Broadcast**: delivers instant messages in scenarios like chat rooms.

* **Presence**: notifies when users are online in chat rooms.

### **AI Assistant**

Capable of full\-stack Supabase function development, PostgreSQL management, service integration, and debugging monitoring.

### **Other modules**

* Advisors: automated suggestions and static analysis that help identify database performance, security, and configuration issues while providing actionable fixes such as missing or duplicate indexes, expired extensions, disabled RLS, or function search_path.

* Reports (reports/observability): visual monitoring dashboards presenting key metrics of database, Auth, Storage, Realtime, Edge Functions, API, and more (CPU, memory, IOPS, connections, requests, error rates, latency, cache hits), supporting different time ranges, source switching, and custom reports (custom reports/dashboards).

* Logs (logs/Logs Explorer): structured logs and a queryable log explorer featuring log tables from various sources (edge_logs, postgres_logs, auth_logs, storage_logs, function_logs, realtime_logs, etc.), supporting SQL query, unnest nested fields, filtering/exporting, templates, and download for event tracing, error localization, and auditing.

> **tip**

> The Logs module of the Supabase console supports querying logs for the last 30 days.
