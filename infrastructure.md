# what a cloud infrastructure provides?
## service registry and discovery
essential as for other parties within to be aware of the service availability at any given time;
also make dynamic resource allocation on the cloud more smooth
## centrol logging
essential for issue tracking and debugging;
combined with alter module, make easy to spot errors and their precise locations & patterns in the cloud environment
## performance monitoring
essential for detecting bottle necks, and where & when to and where & when not to allocation resource

# components
## consul
a consul cluster of 3 machines
### features
* service discovery
* service healthiness check
* internal DNS
* connecting docker swarm

## swarm
a swarm master aggregate of 3 machines
### why?
* a swarm cluster has a dependency on consul cluster for advertising and discovering swarm nodes
* a swarm cluster can create and maintain application-specific interference-free overlay networks
* registrator can be used to collect live container changes and report back to consul, serving as service registry

## load balancers
consul cluster and swarm maters should be accessed respectively via their own load balancers, for any individual node may fail at a given point.

## logging box
### why
centralize log accessing and analyzing

## performance monitor box
### why
monitor server performance and status, in order to properly scale and quickly response to failures.
