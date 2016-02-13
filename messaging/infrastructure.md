
## swarm cluster
a docker swarm cluster of a minimum of 3 machines, sitting at application level.

### key points
* a swarm cluster has a dependency on consul cluster for advertising and discovering swarm nodes
* a swarm cluster can create and maintain specific overlay networks within its topology, therefore allowing related parts of a complex application to communicate privately and securely
* registrator is running as a container on each swarm node, collecting live changes of local containers from that node and report back to consul cluster, so that service could be registered and de-registered
* each application component is running as a container, therefore gets registered as a service within consul cluster; do remember to categorize these services as private/public/etc.

### load balancer
swarm cluster should be accessed via its load balancer, for an individual node may fail at a given point.

## logging collector
collecting application based logs and dispatching them to a central aggregator

## performance monitoring collector
collecting application based performance data and dispatching them to a central aggregator
