# overview
Describe the components of messaging module and the details

# channel types
* **push**        - one-off notification, from server to mobile devices    
* **web socket**  - two-way connection, initiated by client, lasting for an extended period of time




# message protocols
**TBD** - define message formats or protocols for client and server to communicate with, or for messages to be routed within modules. e.g. to specify message type/content/source/destination/expiry/require status report/etc. this protocol should not be mk specific. in fact, the whole system should be built without the knowledge of specific business terms.     
a message contains these fields at least.
1. msg-type
2. source
3. destination
4. appid
5. moduleid
6. msg-text
7. version


need to be intergrated  with the current mobile message (**QRCode scan**, **In-Memory-Text Scan**, **app  invoke**) handle.



 # message types
 * **notification** - instruction or information that business pass out to clients, through either push or web socket channel   
 the count of notification is limited.
 * **chat**         - message from one client to another one or multiple clients, through web socket channel
 * **system control message** -  control messages, through web socket channel, disable the **devices|modules|user**



# message sources
* from queue module, e.g. notification
* from user, e.g. chat   
* from system, e.g. system control message.


# message destination
* to specific user, e.g. A send a message to B
* to specific group, e.g. A send a message to a group named M.DM team.
* to specific system call back handler, e.g.  the client send the log information back to system.
* to device, e.g. try to disable some devices or some broadcast message to all devices.


# message storage
temporarily store messages uploaded from queue module or sent by clients, removed upon delivery, conditionally update delivery status, auto expiration, etc.   
**TBD** - define storage format, state, and process flow diagram(of process unit).

* message id (message which can be read by user)  

* message status    




# message receiver translator
*  convert the **userid** (business user id) to **deviceid** ( generated when app is installed on one    device)
*  check the device status, if it is not **online**, send the message by push notification channel



**the expand message moved to the queue module**
>from tagged message to expanded messages - business would upload mostly tagged messages, which would be >later expanded to address to specific recipients.
>from general message to channel messages - upon delivery, a general message gets translated into channel >specific one, e.g. Apple push notification



## message push
  [**AWS SNS**](https://aws.amazon.com/cn/sns/) -- this will provide us  the ability to send message to mobile devices.



  # components
  1. [balancer](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/balancer.md)    
     a set of api  using by clients before the connection is created.    
     it will assign the most light web socket server to client with the auth token.    
     the client can  use the auth token to generate the connection with assigned server.    
     the detail of balancer please read this document **[balancer]** -- TBD.    

  2. [web-socket servers](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/web%20socket%20servers.md)     
    a set of servers which handle the long-lived connections.
    the detail of long-lived connections please read this document **[long-lived connections]** -- TBD.

  3. [push service worker](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/push%20service%20worker.md)    
     a set of workers which send the push notification by AWS push notification service
     the detail of push service please read this document **[push service workers]** -- TBD.

  4. [api](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/api.md)    
     user: any 3rd part client want to send message to a specific user.
     support send single or multiple messages.

     client: get the message detail by message Id (if the device is not active, we will send the message requests to client by push notification)

  5. [storage](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/storage.md)     
     1. storage all user and device relationship data    
        user    --- Mary Kay user     
        app     --- application     
        device  --- user's device   
        connection ----  the active connection between web-socket server and device
     2. message status
        waiting     
        sent    
        read    
        failed  


  6. [process unit](https://github.com/rongk-team/bex-doc/blob/master/messaging/messaging%20module/components/process%20unit.md)     
     a work flow to control the messaging logic.   
