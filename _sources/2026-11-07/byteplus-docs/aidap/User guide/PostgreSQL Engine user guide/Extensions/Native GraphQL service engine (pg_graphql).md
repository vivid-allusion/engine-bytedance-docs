---
title: "Native GraphQL service engine (pg_graphql)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_graphql"
---

pg_graphql is a powerful PostgreSQL extension that provides a complete GraphQL service engine within the database. With this extension, you can automatically convert existing SQL tables, views, and their relationships into a fully functional GraphQL schema, enabling serverless GraphQL queries.

It builds a seamless bridge between PostgreSQL and GraphQL, allowing any client or programming language that can connect to the database to leverage GraphQL's declarative, strongly typed query advantages without deploying and maintaining additional intermediate services.

<span id="k1xjsw4l"></span>
## Applicable scenarios


* **Rapid prototyping**: provide a fully functional GraphQL API for your database within minutes, accelerating frontend and mobile app development.

* **Simplify backend architecture**: for data\-centric applications, pg_graphql can replace traditional REST APIs or customized GraphQL servers, reducing architectural complexity.

* **Data as a Service (DaaS)** : expose structured data query capabilities securely to internal teams or external partners by treating the database as a service.

* **Integrate with serverless frameworks**: combine with function computing on platforms like Vercel, Netlify, or Supabase to build high\-performance and scalable applications.


<span id="SwX61tzF"></span>
## Precautions

**Primary key requirements**: all tables that need to be exposed in the GraphQL Schema **must** define a primary key. Tables without primary keys will be ignored by the extension and cannot be queried through the GraphQL API.

<span id="AfehU9Ub"></span>
## Create and delete extension

<span id="tEEWqjY7"></span>
### Create extension

Execute the following SQL command to enable the pg_graphql extension.

```SQL
CREATE EXTENSION pg_graphql;
```


<span id="l6bIrG4h"></span>
### Delete extension

If no longer needed, execute the following command to uninstall it.

```SQL
DROP EXTENSION pg_graphql;
```


<span id="AlHYpK0Q"></span>
## Basic usage

The following is a complete getting\-started example:


1. Create table structure

   First, create two tables: accounts and posts, and use foreign keys to establish a one\-to\-many relationship between them.

   ```SQL
   -- create account table
   CREATE TABLE accounts (
       id SERIAL PRIMARY KEY,
       email TEXT NOT NULL UNIQUE
   );
   
   -- create article table and link to accounts table through author_id
   CREATE TABLE posts (
       id SERIAL PRIMARY KEY,
       author_id INT NOT NULL REFERENCES accounts(id),
       title TEXT NOT NULL,
       body TEXT
   );
   ```
   

2. Insert example data

   Insert some data into the tables for subsequent queries.

   ```SQL
   -- insert an account
   INSERT INTO accounts (email) VALUES ('author@example.com');
   
   -- insert two articles for this account
   INSERT INTO posts (author_id, title, body) VALUES
   (1, 'pg_graphql 入门', '这是第一篇文章...'),
   (1, 'GraphQL 查询技巧', '这是第二篇文章...');
   ```
   

3. Execute GraphQL queries

   Use the core function graphql.resolve to execute GraphQL queries. Pass the query statement as a text parameter.

   ```SQL
   SELECT graphql.resolve($$
     query GetAccountsWithPosts {
       accountsCollection {
         edges {
           node {
             id
             email
             postsCollection {
               edges {
                 node {
                   title
                 }
               }
             }
           }
         }
       }
     }
   $$);
   ```
   

4. View response results

   The graphql.resolve function returns a JSONB object containing two fields: data and errors.

   ```JSON
   {
     "data": {
       "accountsCollection": {
         "edges": [
           {
             "node": {
               "id": 1,
               "email": "author@example.com",
               "postsCollection": {
                 "edges": [
                   { "node": { "title": "pg_graphql 入门" } },
                   { "node": { "title": "GraphQL 查询技巧" } }
                 ]
               }
             }
           }
         ]
       }
     }
   }
   ```
   


<span id="o85A6Pqp"></span>
## Core function: graphql.resolve

graphql.resolve is the core function that executes all GraphQL actions.

<span id="1pqCjmz2"></span>
### Function signature

```SQL
graphql.resolve(
    query text,
    variables jsonb DEFAULT '{}'::jsonb,
    "operationName" text DEFAULT NULL,
    extensions jsonb DEFAULT NULL
) RETURNS jsonb
```



* query (text): required, a string containing a GraphQL query, mutation, or subscription action.

* variables (jsonb): optional, a JSONB object providing values for variables defined in the query. Defaults to an empty object ({}).

* "operationName" (text): optional, specifies which named action to execute when the query string contains multiple named actions.

* extensions (jsonb): optional, used to pass data for the GraphQL extensions protocol, typically for advanced toolchain integration.


<span id="e5zq5Y1Q"></span>
### Call examples


1. Query without variables

   The simplest call method is to pass the GraphQL query string directly.

   ```SQL
   SELECT graphql.resolve('{ accountsCollection { edges { node { id } } } }');
   ```
   

2. Use variables

   To improve query reuse and security, using variables is recommended.

   ```SQL
   SELECT graphql.resolve(
       'query GetAccountById($id: Int!) {
         accountsCollection(filter: { id: { eq: $id } }) {
           edges {
             node {
               email
             }
           }
         }
       }',
       '{"id": 1}'
   );
   ```
   

3. Specify action name

   If a request contains multiple actions, specify which one to execute using the "operationName" parameter.

   ```SQL
   SELECT graphql.resolve(
       $$
           query GetAccounts { accountsCollection { edges { node { id } } } }
           query GetPosts { postsCollection { edges { node { title } } } }
       $$,
       '{}',
       'GetPosts' -- specify executing the GetPosts action
   );
   ```
