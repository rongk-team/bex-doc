# use case

## Paul wants to send "hello world" to all consultants
  1. a system message with "consultant" tag send to queue system.
  2. queue system will get the all user list from tag system.
  3. a hello world message will be inserted to each user's queue.
  4. our-message worker will loop each user's queue, package them and send to messaging system.

## A consultant wants to talk with B consultant
   **A** send a user message with the destination "**B**"

## A consultant wants to say something in a group including B,C,D
   1. a group with A,B,C,D is set up by creating a tag named "chat:groupid" which contains A,B,C,D
   2. a user message send with the tag "chat:groupid"

## Eric wants to announce to all directors the newest promotion info
   a system message  with "director" tag  


## Monday wants the device information from mobile devices of shanghai users.
   a system control message with "location:shanghai" tag will be sent    
   the client get the system control message, will call the device collector event.    
   after the info is collected, send it back by call back handler.    


## Frankie wants to do a quick a/b test for active users
  a system control message with "active users" tag will be send.    
  all active client will get the control message .    
  get a small lua script from server    
  change the runtime of client.    
  do the a/b test.    
  collect the result and send it back.  


## one device -- one consultant -- one app
   when the web-socket connection is created and assigned a user. double check the user-device-app mapping data.
   if user has another record already, remove it by a system
   control message
