# overview
Describe the details of balancer


# interaction with client
* send out messages through proper channels



# major prototypes
topology for establishing and load balancing web socket connections, involving client - balancer - front worker
balancer characteristics:
* be aware of front worker load, assign load based on front worker's active connections with clients
* be aware of front worker's topology changes(worker removed, worker added)
