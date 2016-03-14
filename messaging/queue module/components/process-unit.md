 # overview
Describe the outline of the process unit

## workflow

1. Business systems invokes API of the queue module to create a task of delivery messages to users who are of certain tag(s).
2. Process unit retrieves pending tasks from the storage.
3. Process unit call an API of the tag module, telling it what tags there are, then obtain a list of sub list which contains user IDs.
4. Process unit starts serveral in-queue workers and dispatch those sublist to those workers.
5. In-queue workers iterates users in sub lists and save messages into indepent queues for each users.
6. Out-queue works iterates queues which contains pending messages. They send those messages to the message module and clear the queue.

