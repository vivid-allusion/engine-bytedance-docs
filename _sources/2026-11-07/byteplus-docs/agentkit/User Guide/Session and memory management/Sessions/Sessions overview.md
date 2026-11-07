---
title: "Sessions overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Sessions_overview"
---

The Sessions feature is the short\-term memory management capability provided by AgentKit to store and retrieve session context in multi\-turn conversations. With the Sessions feature, agents can persist multi\-turn interaction records between users and agents to a specified database and read historical context in subsequent requests, improving conversation continuity.

<span id="h2UQN2ES"></span>
## Feature overview

The AgentKit Sessions feature supports connecting to BytePlus relational database resources, including **RDS PostgreSQL**, and **RDS MySQL**. You can create or import session resources in the AgentKit console and associate them with the agent runtime for the agent code to read and use.


|**Database type** |**Description** |**Applicable scenario** |
|---|---|---|
|RDS PostgreSQL |An online relational database service provided by BytePlus based on open\-source PostgreSQL, suitable for stable business data read/write workloads. |Scenarios with high access load, large data volumes, or a need for a fixed database instance. |
|RDS MySQL |An online relational database service provided by BytePlus based on open\-source MySQL. |Scenarios where you already have MySQL experience or want to reuse existing MySQL database resources. |


You can use the Sessions feature to:


* Save multi\-turn conversation context to a specified database.

* Use SessionID to distinguish different users or different conversations, avoiding context mixing.

* Continue reading the historical context of the same session when the service restarts, is deployed across multiple instances, or requests are switched to a different runtime node.

* Associate session storage resources with the agent runtime, allowing the platform to inject the environment variables required for database connections, reducing the need to hardcode connection information in your business code.


<span id="Xmne8Rkp"></span>
## How it works

The Sessions feature uses SessionID to identify a conversation session and writes the multi\-turn interaction context of that session to the specified session resource. When a subsequent request carries the same SessionID, the agent can read the corresponding historical context and generate a coherent response based on that historical information.


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

In a typical call chain, a request passes through the following components in sequence:

Client/Application → Agent runtime → Agent business code → Sessions → Session resource database

</card>



The overall workflow is as follows:


1. The client initiates a conversation request, carrying a SessionID that identifies the current conversation.

2. The request enters the agent runtime. If the runtime has an associated session resource, the platform injects the environment variables required for the database connection into the runtime.

3. The agent's business code reads the saved historical context for the session based on the SessionID.

4. The agent passes the historical context together with the current user input to the model to generate the response for this turn.

5. After this turn of interaction is completed, the Sessions feature writes the user input, the agent's response, and the related temporary state to the session resource database.

6. When subsequent requests carry the same SessionID, the agent continues to read the historical context, enabling continuity across multi\-turn conversations.

7. When different users or different business sessions use different SessionIDs, each reads and writes its own corresponding data, avoiding context mixing.


<span id="IVaHmYqb"></span>
## **Core** capabilities and value

<span id="JgsIcwac"></span>
### Maintaining multi\-turn conversation continuity

The Sessions feature writes the conversation history under the same SessionID to the database and reads it for use in subsequent requests. Even if the service restarts or the runtime node changes, the context can be restored based on the same session, reducing information loss during multi\-turn interactions.

<span id="mL63DcRM"></span>
### Reducing the cost of integrating session storage

AgentKit provides unified management for session storage resources:


* **Import resources**: You can import existing RDS PostgreSQL, and RDS MySQL resources.

* **Runtime association**: Associate the session resource with the agent runtime, and the platform automatically injects the database connection environment variables into the runtime, so you do not need to configure database addresses, accounts, or passwords in plaintext in your code.


<span id="5xROyXfz"></span>
### Supporting independent management of business data

Session data is stored in the database resource you choose. Permissions, backup, encryption, auditing, and cleanup policies can all be configured based on the database's own capabilities, meeting your business data management requirements.

<span id="Hp2fOkLj"></span>
### Adapting to multi\-environment and multi\-business isolation

Different businesses and environments can use different session resources, reducing the risk of data mixing and facilitating permission control and O&M management. We recommend generating independent SessionIDs for different users and business sessions.

<span id="6xPBzR5b"></span>
## Concept


|**Concept** |**Description** |
|---|---|
|Sessions |A short\-term memory management capability provided by AgentKit, used to store and retrieve short\-term context across multi\-turn conversations. |
|Session resource |A database resource created or imported in AgentKit, used to hold session context data. Currently supports RDS PostgreSQL, and RDS MySQL. |
|SessionID |A unique identifier for a session, used to distinguish between different users or conversations. AgentKit reads and writes the context of the corresponding session based on the SessionID. |
|Short\-term context |The multi\-turn interaction information within the same session, such as user input, agent responses, and temporary state related to the current turn, scoped to the current session only. |
|Agent runtime |The cloud runtime environment for the agent. Once a session resource is associated with the runtime, the platform can inject the environment variables required for the database connection into the runtime. |
|Memory |Stores long\-term memory information across sessions, independent of the short\-term context capability of the Sessions feature. |
|Knowledge Base |Stores and retrieves knowledge content such as enterprise documents and business materials, designed for RAG scenarios, distinct from the short\-term context storage capability of the Sessions feature. |


<span id="RKImaGri"></span>
## Data storage boundaries

Sessions, memories, and knowledge bases address different types of data storage needs. Their content and lifecycle are different. We recommend choosing the appropriate capability based on your business objectives.


|**Module** |**Stored content** |**Lifecycle** |
|---|---|---|
|Sessions |Multi\-turn Q&A records for a single session, SessionID, and temporary state related to the session. |Typically tied to the session lifecycle. The specifics depend on product configuration or database\-side configuration. |
|Memory |Long\-term memory information across sessions, such as user preferences and long\-term profiles. |Independent of the session lifecycle. It must be managed or deleted using the memory's capabilities. |
|Knowledge Base |Knowledge content such as enterprise documents, business materials, and vector indexes. |Independent of the session lifecycle. It is maintained based on the knowledge base's document management policy. |


<span id="WRNyiPNv"></span>
## Applicable scenario


|**Scenarios** |**Criteria** |**Role of Sessions** |
|---|---|---|
|Multi\-turn continuous conversations |Users need to continuously reference prior information across multiple turns. |Stores and retrieves historical context to improve conversation continuity. |
|AI applications deployed across multiple instances |The application is deployed across multiple runtime nodes, and requests may be forwarded to different nodes. |Uses a unified database to store session data, reducing context loss caused by node switching. |
|Businesses that need to independently manage session data |The business needs to manage permissions, backup, auditing, or cleanup policies on its own. |Stores session context in the specified database resource, making it easy for the business to maintain. |
|Lightweight, fast launch of agents |You want to reduce database O&M work and need elastic resource usage. |Choose RDS PostgreSQL to hold session data, lowering resource preparation and O&M costs. |
|Reusing existing database resources |You already have RDS PostgreSQL, or RDS MySQL, and want to continue using your existing database system. |Imports the existing database resource into AgentKit for use as a session resource. |


<span id="v63JB2xa"></span>
## Procedure


1.  ** ** [Import a session resource](https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources): Import a session resource in the AgentKit console. The session resource is used to read and write the short\-term context of multi\-turn conversations.

2. [Integrate session management capabilities into your agent code](https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents?lang=zh&TagIDs=2,484,400#3qaSIptE): Use SessionID to read and write context.

3.  **(Optional) Local testing**: Use the same SessionID across multiple test turns to confirm that the context is saved and read correctly.

4. [Deploy the agent to the production environment](https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents?lang=zh&TagIDs=2,484,400#UZPKgtkj): Deploy the agent to the agent runtime, using the session resource to hold production session data.

5. [Associate the session resource with the agent runtime](https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents?lang=zh&TagIDs=2,484,400#Wd0sb4og): On the component association page of the agent runtime, associate the session resource. After the association, the platform automatically injects the database connection environment variables and component invocation capabilities.

6. [Publish the runtime](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes): After associating the session resource with the agent runtime, you also need to manually publish the agent for the new configuration to take effect.
