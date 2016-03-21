# overview
The primary goal of the queue module is that process requests of deliverying messages and delivery those messages to the message module.

There are five components:

[API](components/api.md)

API provides public functions to accept requests which come from business systems to delivery messages to users of specific tags. 

API saves requests as tasks and dispatch them to process units.

[Process Unit](components/process-unit.md)

Process unit processes pending tasks of deliverying messages which are created by API.

It divides tasks into small sub-tasks then dispatch them to in-queue workers.

[In-Queue worker](components/in-queue-worker.md)

In-queue workers iterates users in the sub tasks then save messages into indepent queues for each users. Those messages wait for pick-up by out-queue workers.

[Out-Queue worker](components/out-queue-worker.md)

Out-queue worker iterates message queues then send those messages to the message module and clear the queue.

[Storage](components/storage.md)

Defines entities.
