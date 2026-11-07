---
title: "Using Realtime"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Realtime"
---

This topic introduces how different roles use the Realtime function module.

## Background

The Supabase console provides real\-time message communication and broadcasting through the Realtime component. The client connects to Realtime via WebSocket. Combined with PostgreSQL database’s built\-in logical replication slot and trigger, and by monitoring changes in Realtime’s messages system table, record updates in the database can be pushed in real time to multiple clients.

## Debug Realtime subscriptions in the Supabase console

### Prerequisites

* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

### Procedure

1. In the Supabase console, click **Realtime** on the left to enter the **Realtime** page.

2. On the **Realtime** page, select **Channel** and **Role** to start listening to the specified channel.

   > **tip**

   > On the **Realtime** page, you can also configure filters for listening and initiate broadcasts. For more details, refer to [Realtime](https://supabase.com/docs/guides/realtime).

   ## Create a Realtime subscription through the Supabase Client SDK

### Prerequisites

Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

### Procedure

1. Subscribe to database changes.

```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// subscribe to database table changes
const channel1 = supabase.channel('db-channel')
channel1
  .on('postgres_changes', {
    event: '*',
    schema: 'public',
    table: 'mytable'
  }, payload => {
    console.log('mytable changed: ', payload)
  })
  .subscribe()
```

2. Subscribe to Broadcast.

```JavaScript
// subscribe to broadcast messages
const channel2 = supabase.channel('broadcast-channel')
channel2
  .on('broadcast', { event: 'message' }, payload => {
    console.log('received: ', payload.payload)
  })
  .subscribe()

// send message
channel2.send({ type: 'broadcast', event: 'message', payload: 'hello' })
```

3. Subscribe to Presence.

```JavaScript
// subscribe to online status
const channel3 = supabase.channel('presence-channel')

channel3
  .on('presence', { event: 'sync' }, () => {
    const state = channel3.presenceState()
    console.log('在线用户', state)
  })
  .on('presence', { event: 'join' }, ({ key }) => {
    console.log(key + ' 上线了')
  })
  .on('presence', { event: 'leave' }, ({ key }) => {
    console.log(key + ' 下线了')
  })
  .subscribe(async status => {
    if (status === 'SUBSCRIBED') {
      await channel3.track('user123', { name: '测试用户' })
    }
  })
```
