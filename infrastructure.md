# what should cloud infrastructure provide?

## service registry and discovery
it's essential to know what service and to what degree a service is available at any given time;
also, it makes dynamic computing resource allocation on the cloud more smoothly

## central logging
it's essential for issue tracking and debugging

## performance monitoring
it's essential for detecting system bottlenecks, so that questions like where & when to and where & when not to allocation resource could be answered with confidence;

# proposed components

## consul cluster
a consul cluster of a minimum of 3 machines, sitting at data center level.

### features
* service discovery
* service health check
* internal DNS lookup
* facilitating docker swarm discovery

### api
a set of api is required to provide service query and update, including availability, health status, utilization, etc.
could be an independent api based on what consul has already provided.

## load balancer
consul cluster should be accessed via its load balancer, for an individual node may fail at a given point.

## logging aggregator
centralize log accessing and analyzing
may use open source products or equivalents provided by cloud service provider

## performance monitoring aggregator
centralize server performance and status, in order to properly scale and quickly response to failures
may use open source products or equivalents provided by cloud service provider
