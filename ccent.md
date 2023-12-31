# CCNA CCENT Networking course

# Chapter 2

## IOS: internet network operating system

core building blocks of network
- switch: communication between local area network
- routers: communication between wide area network
- wirless access point
- client and server



# Chapter 3
## OSI model
- A standard architecture defining network communication
- A system to "break down" network communication
- A standard to create standards
- A competing protocol to tcp/ip

## layers
- application
    - what is application itself iterfaces with it it's network aware
    - world of warcraft, google chrome, API, etc...
    - clients and servers

- presentation
    - generfies the data
    - encryption
    - clients and servers

- session
    - end session, make sure session is active, create session ids in operating system, etc ...

- transport
    - how the data is set
    - application said i want send it reliably or onreliably (tcp/udp)
    - ports [1,65535]

- network
    - logical addressing (IP)
    - routers

- data link
    - physical address (MAC)
    - we need to provide source IP, destination IP, source MAC and destination MAC
    - switches, wifi

- physical
    - hub
 

## IP and MAC
### IP 
Final desitnation of data. show end to end address
### MAC
Address in local area network, changes in data journy, but IP is same

### Encapsulation
Adding data to front of payload

### Pots
1-1024: well known

## find routers when request data
```bash 
traceroute google.com
```
 
# Chapter 4
## IP
four octet, each from value between 0, 255, combined with "subnet mask" and usually, "default gateway"

## subnet mask
defines your neighborhood

### example
    172.30.100.30
    255.255.255.0

## 255
what is the "network" 
## 0
host; who am I
## example
in a local network, the 172.30.100.30 wants to send data to 172.30.100.150, steps are:
- send broadcast, using ARP (address resolution protocol) to find MAC addrress
- the devices that is not that IP, ignore broadcast, but device with this IP, recives broadcast
- the destination IP sends direct message to source IP, containing MAC address
- the destination IP, source IP, destination MAC and source MAC collected
- switch sees MAC address and sends data

## MAC Address
12 charachter hexadecimal

**hint: switch sees only MAC addresses**

## default gateway
communicate with IPs that is not in the neghiborhood
### steps
- ARP to get that IP
- the IP is not in the neghiborhood, so the arp stops in default gateway (or router)
- the destination IP, source IP, destination MAC (default gateway) and source MAC collected
- switch sends data to router
- router uses his routing table to find destination network
- sends data to destination netowk
- destinatin router tares off source and destination MAC address and replace with source router MAC and destination route MAC
- destinatin router sends arp to find MAC of destination IP and sends data IP

## default route
0.0.0.0 this is internet

## BGP
know every single network in the internet. most routers didn't have memory capacity of it

# 5
## IP addressing
- static
  - servers, printers, routers
- DHCP (dynamic host configuration protocol)
  - when new computer boots, it sends broadcast and gets IP
- DHCP relay
  - used when different networks with different routers wants to get IP
  - it elables in each router and sends ONLY DHCP broadcast to main DHCP server
- multiple IP address

## public and private IP addresses
### private IP addresses
- 10.0.0.0 through 10.255.255.255
- 172.16.0.0 through 172.31.255.255
- 192.168.0.0 throught 192.168.255.255

#### NAT
network address translation
translate IPs in network to one public address

### automatic addressing
169.254.0.0 through 169.254.255.255
will generate if can't contact a DHCP server

### loopback addressing
internal IPs of device

### special addresses
first and last address of the subnet = network and broadcast


## classess of addresses
class A: 001 - 127, subnet mask: 255.000.000.000 (/08)
class B: 128 - 191, subnet mask: 255.255.000.000 (/16)
class C: 192 - 223, subnet mask: 255.255.255.000 (/24)

we can use another subnet mask of classes for specific class, but we must go further, not backwards
for example, we can use IP of class A with subnet mask of class C, but
we can't use IP of class C with subnet mask of class B

practically, we cant use subnet mask of class A in IPs of class A, because it will flood the network, for example: broadcasting

class D: 224 - 239 (multicast)
class E: 240 - 254 (experimental)

kinds of communication
- unicast (message to one)
- multicast (message to group of devices)
  - imaging, a server with windows image and 5 computers connectted to that server
- broadcast (message to everybody)
 
# 6
## TCP
reliablility in communication
HTTP is A TCP based protocol

### 3 way handshake steps
- SYN: sends SYN packet: I would like to start discussion with you 
- SYN / ACK: yes. I got you and here is mine
- ACK: i got your SYN

### TCP window size
when a computer wants to send file, it first sends 1 packet and recives ACK.
if all packet sends successfully, it increases number of packetes, until
there is a problem
### sequence number
computer sends number of packets and start incrementing if bandwidth is awailable
the server that recieved packet, sends acknowledgement sequence number, meaning that expectes sequence number of computer
packet size: 1500 bytes

## UDP
unreliablility in communication
voice over IP (VOIP)

### DNS
domain name server
the DNS needs UDP connection
#### types of finding IP 
- recursive
  - look for it's parent
- iterative

after get the IP, it cache it's value

### hints
- the "A" suffix requested from dns server is for IPv4. for example: we request blah.com, it request A blah.com from dns to get ipv4
- the "AAAA" suffix requested from dns server is for IPv6



# 7
## ports
from 1 to 65535
## well known ports
to 1023
## common TCP ports
- FTP (file transfer protocol):         21
- SSH:                                  22
- TELNET:                               23
- SMTP (simple main transfer protocol): 25
- DNS SERVER:                           53
- HTTP:                                 80
- POP3 (email clinet):                  110
- HTTPS:                                443
- IMAP:                                 143


## common UDP ports
DNS client: 53
69: TFTP

## differnce between TFTP and FTP
FTP needs username and password, but TFTP is not login required

## Frame in packet
FCS (frame check sequence) or CRC (cyclical redundany check)
Any network card takes whole packet and gives a hash and puts in packet
the destination takes all information of packets and generates the hash
and checks with the hash exists in packet. it match, it is a good packet,
if not, the destination drops that packets
reasons: malicious behaviour, man in the middle, electro megnatic interference, etc ...

## hint
data is differnt names when passes to each layer except app layer (application, presentation, session)
- transport:  segment
- network:    packet
- data link:  frame
- physical:   bit


# 17
## how routers works

we have two networks
- 192.168.1.0/24
- 192.168.2.0/24

the 192.168.1.1 tries to reach 192.168.2.50
the 192.168.1.1 can't send arp, because the destination is not exists in it's network
mac address: 
192.168.1.1     1111
router          2222


steps
- sends arp to himself and gets default gateway
- assemble a packet: {source: 192.168.1.1, destination: 192.168.2.50, source_mac: 1111, destination_mac: 2222}
- router looks in it's routing table
someone configured the routing table as follows:
192.168.2.0/24        10.1.1.0/24
if the requested ip didn't exist in routing table, then the packet drops
- fills source_mac in destination_mac with the source_route_mac and destination_route_mac
- the destination route gives packet to the destination ip
- in order to full communication, the destination route needs to know the source route, ways are
  - static routing
  - dynamic routing

## IOS powered
routers run on software. its the brain 

## CEF enhnaced
Cisco Express Forwarding (CEF) is the most widely used forwarding mechanism on IP 

# 32: NAT concepts
NAT: network address translation
private ips
10.0.0.0    10.255---
172.16.0.0  172.31.255.255
192.168.0.0/16
the standard is: RFC 1918

## types of NAT
### static
one to one mapping that dosen't change

### dynamic
### PAT
uses open port of client and translates to the route public address with this port
what if two client opens same port and want to get data
for example: port=6711
router gives data to one client and incruments the port number and gives data to other client

# 34 IPv6
why we need IPv6
- there is IP address shortratge
- current IP address poorly allocated
- new network devices on the rise
- NAT is now seen as a hinderence to innovation
- potential future features: ipsec everywhere, mobility, simpler header

IPv6: 128 bits, 8 octets, each part represent 16 hexadecimal bits
example: 2001:0050:0000:0000:0AB4:/E2B:98AA

**Rule 1**: zeros can be groups together using ::
2001:0050:0000:0000:0AB4:/E2B:98AA -> 2001:0050::0AB4:/E2B:98AA
**NOTE**: you can use :: one one time in 

**Rule 2**: drop leading zeroes


2001:0050:0000:0000:0AB4:/E2B:98AA -> 2001:50::AB4:/E2B:98AA

IPv6 header is more simpler

## types of communication and addresses
- unicast: one to one
- multicast: one to many
- anycase: one to closest
- broadcase: are GONE!

## link local scope address: layer 2 domain
works in local communication.
let's create ip address for communication in a switch infrastructure, then
the system generates ip with FE80: in the begining (FE80::/64)

FE80::/64
the first 64 bits is network
the system can auto configure itself (stateless configuration) with it's own host id
most common way is EUI-64
### EUI-64
im going to use my MAC address to create Host ID
example: MAC=11:22:33:44:55:66
- add in the middle: FFFE
- result = 1122:33FF:FE44:5566
- add FFFE in the middle
- and so on, until it create IPv6 

### summary
- assigned automatically as an IPv6 host comes online
- similar to the 169.254.x.x addresses of IPv4
- always begin with "FE80" followed by 54 bits of zeroes
- the last 64 bits is the 48 bit MAC address with FFFE squeezed in the middle


## unicode/site local scope address: organization
this our private addresses


## global scope address: internet
have their high level 3 bits set to 001 (2000::/3)
there is an organization names IANA, who can give IPv6 to servers
### global routing prefix is 48 bits or less
example
- the IANA give prefix 2000:1111:2222 to organization1
- the IPs for three device example is
  - 2000:1111:2222::0001
  - 2000:1111:2222::0002
  - 2000:1111:2222::0003

the calculation of subnet is: 64 - (number of prefix bits)


### subnet ID is comprised of bits are left over after global routing prefix

### the primary addresses expected to comprise the IPv6 are from the 2001::/16 subnet
- /32 subnets assigned to providers
- /48, /56, /64 subnets assigned to customers
