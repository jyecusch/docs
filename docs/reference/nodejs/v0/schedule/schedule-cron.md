---
title: Node.js - schedule.cron()
description: Reference for Nitric's Node.js library - Sets the frequency and one or many handlers to be triggered.
---

Creates a cron expression based schedule and one or many handlers to be triggered.

```javascript
import { schedule } from '@nitric/sdk';

// Create a schedule that runs everyday at 7:00am
schedule('morning-reminder').cron('0 7 * * *', async (ctx) => {
  // do some processing
});
```

## Parameters

---

**expression** required `string`

The cron expression to use to define when the schedule's handlers should be triggered.

**middleware** required `EventMiddleware` or `EventMiddleware[]`

One or more middleware functions to use as the handler which will run on defined frequency.

---

## Examples

### Create a Schedule to run every hour

```javascript
import { schedule } from '@nitric/sdk';

// Create a schedule that runs every hour on the hour
schedule('send-reminder').cron('0 * * * *', async (ctx) => {
  // code which sends a reminder
});
```
