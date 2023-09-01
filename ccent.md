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

find routers when request data
traceroute google.com
 
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
