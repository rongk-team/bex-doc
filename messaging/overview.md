# overview
TBD - define interface and data flow among sub modules, with external systems(client devices, other service or api owned by business)

## system characteristic
Long-lived connections are established and maintained between clients and servers for passing messages.
Given that each client comes online randomly, therefore evens out each one's chattiness,
it is then the quantity of such connections that matter the most, in terms of mounting system pressure.
So a strategy based on the number of connections should be devised in order to maintain and balance load among servers.

# sub modules

## messaging module

### channel types
* push        - one-off notification, from server to mobile devices
* web socket  - two-way connection, initiated by client, lasting for an extended period of time

### message types
* notification - instruction or information that business pass out to clients, through either push or web socket channel
* chat         - message from one client to another one or multiple clients, through web socket channel
* ???? message - TBD other types of message/instruction, through web socket channel

### message protocols
TBD - define message formats or protocols for client and server to communicate with,
to specify message type/content/source/destination/expiry/require status report/etc.

### message sources
* queue module, e.g. notification
* clients, e.g. chat

### message storage
temporarily store messages from queue module or clients, delete upon delivery, update delivery status, auto expiration, etc.
TBD - define storage format, state, and process flow(a process unit).

### module scope
TBD - confirm if push channel is within current development scope or it is already exist?

### interface to queue module
* upload messages - uploaded messages will be processed immediately, through push channel if no web sockets are available.
* query status    - queue module use to query delivery status if the message uploaded marked as require status report.

### interface to client
* request new web socket channel with web socket load balancer(caps applied? no more than 1 connections allowed from the same ip?)
* establish assigned web socket channel with one of the front web socket workers

### interaction with client
* send out messages through proper channels

### interaction with tag module
* expand messages, call upon the tag module to expand a tagged message into a concrete message set
(implying a two-level, abstract-concrete message storage hierarchy)

### interface authentication
* with client       - ??? with load balancer; token based authentication with front workers.
* with queue module - network based security
* with tag module   - network based security
TBD - define authentication details

### prototyping
TBD - test out topology for establishing web socket connections, client - balancer - front worker
balancer characteristics:
* be aware of front worker load, assign load based on front worker's active connections with clients
* be aware of front worker's topology changes(worker removed, worker added)

### components
balancer - contains client api
front worker - contains client api
storage - contains queue api
message processing unit - connect storage, balancer, and front worker to direct message flow

## queue module
message addressed to specific recipients
message addressed to specific tags
message addressed to some tag combination, e.g. tag_A + tag_B, tag_A - tag_B

### queue storage
* store tagged message
* store tagged message delivery status

### queue processing unit
* schedule massage upload
* pull message delivery status
* other massage status, storage maintenance

### interface to business
upload message - allow business to upload tagged message, specify priority, time to send, etc.
cancel message - only those messages which have not been uploaded to the messaging module could be canceled.
prioritize message - update uploaded message's priority field
query message delivery status - query uploaded message's delivery status, sent/not sent/delivery percentage/expansion count/etc.

### interaction with messaging module
upload message - when the tagged message is due for delivery, upload it for immediate sending
query message delivery status - query and update message delivery status to storage

### interaction with tag module
validate tags - upon uploading message, validate message tag consistency

## tag module

### tag storage
* store tag meta data
* store tag - client mapping, it's better to use an immutable data structure here

### interface to business
manipulate tag - tag creation/update/delete/etc.
tag operation - create tag alias, tag combination, etc.
manipulate tag mapping - manage tag - client mapping, is it possible for business to upload a mapping delta?

### interface to queue module
validate tags - validate tag existence, and the like

### interface to messaging module
validate tags - validate tag existence, and the like
expand tag - expand a combination of tag into client mapping
(for performance sake, might give messaging module direct access to an immutable tag mapping, allowing expansion operation extra fault tolerance)

### prototyping
tag redis data structure?

# optimized timeline & estimation
* fast sub system concept/topology prototyping
* interface prioritized
* fast and continuous test & deployment

# iteration and output
TBD
