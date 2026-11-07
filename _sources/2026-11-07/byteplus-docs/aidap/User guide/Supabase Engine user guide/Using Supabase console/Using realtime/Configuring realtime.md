---
title: "Configuring realtime"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuring_realtime"
---

Realtime settings configure the enable status of the Realtime service, channel access strategy, connection pool size, and event quota in the current workspace. After adjusting the configuration, the system disconnects the currently connected Realtime clients, so the Realtime service reinitializes with the new configuration.

## Prerequisites

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* The current account has permission to manage Realtime configurations.

* To verify the configuration effect, ensure that the business client has connected to Realtime.

* Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

## Precautions

* After saving the Realtime configuration, currently connected Realtime clients will be disconnected. The clients need to reconnect to use the new configuration.

* After disabling the Realtime service, new connections will be rejected and connected clients will be disconnected. Keep the Realtime service enabled if you need to continue using Broadcast, Presence, or Postgres Changes.

* After disabling public channel access, clients need to pass Realtime Authorization verification when joining channels. If private channel configuration is not set or corresponding access Strategy is not configured, clients may not receive messages.

* Connection pool and quota configuration affect Realtime's connection capacity, message throughput, and resource consumption. Adjust according to business concurrency scale and pressure test results.

## Procedure

1. In the Supabase console, select **Realtime**.

2. In the Realtime page left navigation bar, select **Configuration** \> **Settings**.

3. Configure Realtime parameters as needed. For detailed information on the parameters, refer to [Parameter description](https://docs.byteplus.com/en/docs/330/123467#6VKYLYDr).

4. Click **Save changes**.

## Parameter description

|**Parameter** |**Default value** |**Tip** |
|---|---|---|
|Realtime service |Enabled |Control whether to enable Realtime service. When enabled, the client can establish Realtime connections normally; when disabled, connected clients will be disconnected and new connections will be rejected. |
|Allow public access to channels |Enabled |Control whether clients are allowed to access public channels. Enabled: the function is enabled. Clients holding the project's anon key can subscribe and broadcast public channel messages; when disabled, clients must pass private channel authorization checks to join channels. |
|Database connection pool size |1 connections |Database connection pool size used by Realtime Authorization. This connection pool is used for private channel joins, access token Refresh, and RLS verification in private Broadcast REST requests. A value too low may cause authorization verification to queue or time out; a value too high consumes database connections. |
|Postgres Changes connection pool size |4 connections |Connection pool size used when creating Postgres Changes subscriptions. This connection pool is used for creating subscriptions and is different from the connection used for continuous change data transmission. If the value is too low, burst subscriptions may time out during creation. |
|Max concurrent clients |200 clients |The current workspace limit on the number of simultaneous Realtime clients connected. One WebSocket connection counts as one client, regardless of how many channels it joins. New connections are rejected after reaching the limit. |
|Max events per second |100 events/s |The current workspace's maximum allowed event processing rate per second. Events include messages sent by clients and messages dispatched from the server to clients; a broadcast message sent to multiple subscribers counts as multiple events based on the number of dispatches. |
|Max presence events per second |1000 events/s |The current workspace's maximum number of Presence events allowed per second. Presence track, untrack, and synchronization events all count toward this limit. |
|Max payload size (KB) |3000 KB |The maximum payload size allowed for a single Realtime message. Broadcast or presence messages exceeding the limit may be rejected or cause the channel to close. |
