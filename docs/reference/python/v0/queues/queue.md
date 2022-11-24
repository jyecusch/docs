---
title: queue()
description: Creates a new Queue to send and receive asynchronous tasks.
---

Creates a new Queue to send and receive asynchronous tasks.

```python
from nitric.resources import queue

batch_queue = queue('batch').allow('sending')
```

## Parameters

---

**name** required `string`

The unique name of this Queue within the app. Subsequent calls to `queue` with the same name will return the same object.

---

## Access

All Nitric resources provide access permissions you can use to specify the level of access your code needs to the resource. See here for details [Access Control documentation](./../access-control).

### Available permissions:

---

**sending**

This permission allows your code to send new tasks to the queue.

---

**receiving**

This permission allows your code to receive tasks from the queue.

---

### Notes

In most instances code should either send to or receive from a queue, usually not both.

## Examples

### Create a Queue

```python
from nitric.resources import queue

batch_queue = queue('batch').allow('sending')
```

### Send tasks to a queue

```python
from nitric.resources import queue
from nitric.api import Task

batch_queue = queue('batch').allow('sending')

payload = {}
await batch_queue.send(Task(payload=payload))
```

### Receive tasks from a queue

```python
from nitric.resources import queue

payload = {}
batch_queue = queue('batch').for('receiving')

tasks = await batch_queue.receive(10)
```