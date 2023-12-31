source: [ITkFunde](https://www.youtube.com/@ITkFunde)

# load balancing
- can be setup in layer 1 or layer 4 of OSI model
- uses see single anycast IP



## algorithms for load balancing
### round robin
DNS servers use this

### weighted round robin
can we weigthed based on cpu, memory, etc...

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
- layer 2/3 
  - low intelligence
  - uses ARP, ICMP, ...
- layer 4
  - mediom intelligence
  - uses TCP, UDP
- layer 7
  - high intelligence
  - application level health check
  - http/https



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

# availability vs durability
example
assume two bank, represent availability and durability

availability                    durability
bank1                           bank2
24/7 available                  3 days a week
3 theft                         0 theft

any bussiness shoud choose durability over availability if there is a choice

# proxy vs vpn
proxy                                                   vpn
hides identitiy                                         hides identitiy & information
hides your ip                                           hides your ip + encrypt data
for web traffic (http)                                  all kind of traffic (http, udp, etc...)
less secure                                             more secure
works at application level                              works at os level
less reliable                                           more reliable
easy to maintain                                        hard to maintain
cheaper                                                 expensive
can face performance issue if you use shared proxy       can face performance issue depends on distance of vpn client and vpn server

# new load balances
what load balancers do
- balance the load
- ADC: **A**pplication **D**elivery **C**ontroller

## basic concept
### reversse proxy
a web server between client and backend server
DSR: direct server return, meaning the backend server can talk directly to client

### VIP
virtual IP

### connection table
5 tuple connection table. 5 ingredient with basic information each load balancer should have
- source IP
- destination IP
- source port
- destination port
- protocol

### traffic distribution algorithm
<a name="algorithms for load balancing">talked here</a>

## ADC benefits

old load balances gives us only availability
but ADC gives:
- availability
- agility
- efficiency
- security

## ADC capibility
### content switching
what kind of content should route to backend server
for exampe, jpg routes to jpg server

### gloabl server load balancing (GSLB)
handles the traffic when one backend server goes down

### edge authentication
handle user authentication. no need for backend server to authenticate

### web application firewall (WAF)
- OWASP 2021 top 10
- HIPPA
- PCA DSS
  
### what LB has and what ADC added
- LB
  - reverse proxy
  - availability
  - health checks
  - LB algorithm
- ADC
  - content switching
  - global server load balancing (GSLB)
  - edge authentication
  - WAF
  - network telementary
    - proccessing of collecting network metadata, aggregating and analyzing data
  - ssl/tls encryption offload
    - all encryption can be handled by load balancers
  - compression
    - enhance the performance



# NAT (network address translator)
we have a office with 3 developers, we can't assign ip to each developer because:
- IP is expensive
- impossible, because of IP constraint

solution: every developer have private IP and they use office public IP

question: what happens when someone tries to communicate with the IP outside of netework?
answer: the router acts as NAT

## typs of NAT
### static NAT
very basic
maps every private address to global address

### dynamic NAT
dynamically assigns the public IP to whichever request comes to the nat device first

### nat overloading
we further utilize the publicly reserverd IP based on the ports using PAT (port address transator) table
example
developer1: 10.0.0.1
developer2: 10.0.0.2
developer3: 10.0.0.3

PAT table
inside          outside
10.0.0.1        125.10.12.13:5001
10.0.0.2        125.10.12.13:5002
10.0.0.3        125.10.12.13:5003

## how NAT works
assume NAT table

inside realm        outside realm
10.0.0.1            123.10.12.13

steps
- private IP wants to communicate to internet
- send request to NAT
- packet: source: 10.0.0.1, destination: 123.10.12.13

# SSO (single sign on)
your identitiy authorized right at the entrance
## how SSO works
### SAML
sequrity assersion markup language: open standard exchange identity between identity provider and service provider
example:
- identity provider: goverment
- service provider: wedding menu
 
silent single sign on: no need password

# Networking basic concepts
## DMZ
demilitarized zone: zone created within local area network where in it a specify to the router that whenever any adhoc external network connection wants to try establish connection through local area network, you simply pass connection to the DMZ  
## Port forwarding

# network hub and spoke
centeral device (hub) conencted to multiple other devices (the spokes)


# how routing works
## routing table
a table for each router that shows what is the next destination for specific requested IP
assume a system requests to 10.0.0.1
the routing table as follows
IP            route number
12.32.42.52   #2
10.0.0.1      #3
so, the router decides to route request to router #2
the router 2 follows these steps too.

## types of routing
### static routing

### dynamic routing
#### autonomous system
collection of routers
#### interior GW protocols
inside autonomous system
##### distance vector
protocol: RIP
very old protocol
the router only knows the next router based on distance calculated
##### link state
protocol: USPF
opposite of distance vector
the origin router will have all the understanding of path. it will be faster
##### hybrid
protocol: EIGRP
mix of both
#### exterior GW protocols
outside autonomous system
##### path vector
protocol: BGP
very close to distance vector
the protocol will need whole path to be shared, and then it will calculate how to reach destination


# MTLS
mutual TLS
the TLS is server authenticating to client
MTLS is about not only client trust the server, but also the server trusts the client
## why we need MTLS
with the change of how we build applications and with the change of how we access application, 
mtls is become to more important
### use case
currently our apps become lots of microsevices talking to each other
we want to make sure only valid components can talk to each other
so now a hacker cant pretend to be a middleware

## downsides
- communication heavy 
- performance issues

