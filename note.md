# ND/NS
the procedure of communicating via IPv6



# BGP (border gateway protocol)
- is a protocol used by routers on the internet to figure out the best way to send data between different networks
- routing protocl
- path vector protocol
- tool for internet service providers

## AS (autonomous system)
- the independent operated computers that creates internet networks
- routers and networks under a single administrative control
- example: ISP with companies
  - an ISP hold two companies: c1 and c2
  - it assign a unique number to each company. the number is AS number
- example: multipe ISP with multiple company
- some companies with different ISP an create a private AS
## edge



## how BGP works
there are some AS around the world. they have some edge server to communicate to each other
they have peer agreement with each other in order to create a network graph around the world
so if we request to specific IP, the BGP find out what is the best path in order to get
the data
each AS will advertise some routes
the route length is an attribute that BGP looks in order to get best route

## IPG
## EGP
## hup or hop


# dynamic routing protocols
router automatically share routes with each other
example
- Company A as an autonomous systerm
- Company B as an autonomous systerm
## protocls
### IGP (interior gateway protocol)
- designs for inside autonomous system
- speed
- responsive
- stability: if something wrong happend to a route of company, all routes must know about it
#### distance vector
- only have knowladge of next hop
- less ram and CPU
- slower convergence
##### RIP (routing information protocol)
##### EIGRP (enahanced interior gateway routing protocol)
#### link state
- have knowladge about entire network topology
- all routers know what router they connected
- cost more ram and CPU
- 
##### OSPF (open shortest path first)
##### IS-IS (intermediate system to intermediate system)
### EGP (exterior gateway protocol)
- between AS
#### BGP (border gateway protocol)
- most companies share IP address with ISP
- each company connects to one or more ISP and share thier route with ISP
- the internet is bunch of ISP connected to each other
- each ISP shares routes with each other and different companies with BGP
- tunded for stability: if something wrong happend to a route of company, all routes in interior network must know about it, but we dont need to flood the internet about some small thing
- security
  - for example, the ISP handles company A with a router
  - if company A must do melicious, the ISP will reject request of company A
- gives company B the ability to share route with different ISPs in order to create path from outer to connect to company B