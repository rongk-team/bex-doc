# overview
Describe the process unit of messaging

## connection create process

1. client send request to web-socket server use the auth token assigned by balancer.
2. web-socket check the auth token, if pass, create a long-lived connection with client.
3. web-socket server store the connection id, user id, and device id into db.



## messaging process

1. queue system send the message request to api
2. do the message translator process
3. if user is active, send the message by connection
4. if user is not active, send the message to push service worker
