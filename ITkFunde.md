source: [ITkFunde](https://www.youtube.com/@ITkFunde)

# load balancing
- can be setup in layer 1 or layer 4 of OSI model
- uses see single anycast IP



## algorithms for load balancing
round robin
DNS servers use this

### least connection
which node has less connection and pass request to partucual server
suitable for backend server

### least response time
which node has least response time and pass request to partucual server

### least bandwidth
which node has least bandwidth and pass request to partucual server

### hashing
---

## types

### internal LB

### external LB

## components
### global forwarding rule
### target proxy
### URL MAP
### backend service
### health check


# firewall
## types
### packet fitening
inspect any packet, checks source, destination, port and etc
#### goods
very cheap
very efficient
#### bads
insecure, vulnerable against IP spoofing
IP spoofing
somewone injects IP

### stateful inspection
the firewall also checks overall contexts
keeping previous packets and coming packets

### circut level gateway
a tunel between source and destination
conencts both of network at once, and goes out
VPN is kind of it

### application proxy gateway
combines all good of previous types and offers more
works at application layer of OSI
takes application context, and deployes firewall rule

### firewall as a service (FaaS)



# edge computing
why we want edge computing
- latency
- processing

