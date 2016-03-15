# overview
Describe the details of api


## api for mobile app
these apis will assign a user to one active connection.
 1. client send device/application information to web-socket server.
 2. if accept, mark connected.
 3. client sent a request with access_token to web-socket server when connected and authenticated.
 4. web-socket server will check the access_token
 5. if pass , mark this connection with the user id



## api for queue system
  accept the message sending request from queue system
