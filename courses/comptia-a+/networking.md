# Important terms

- TCP(Transmission Control Protocol), connection-oriented , "reliable" delivery , eg. loading a website
- UDP (User Datagram Protocol) , connectionless ,"reliable" delivery , eg live-stream
- IP address = which house
- Port = which room
- Non-ephemeral ports (0-1,023) = permanent port numbers , eg. 80 for web servers and port 443 for HTTPS
- Ephemeral ports (1,024-65,535) = temporary port numbers (servers mostly use these)

## Network devices

- Router : A router routes traffic between IP subnets
- Subnet : seperate larger network into smaller, manageable segments
- Switch : Provides physical connections between network devices within a LAN
- Patch panel : organise network cables , many desktops to one patch panel
- PoE (Power over Ethernet) : for telephone , PoE
- Hub (old , before switches) , inefficient
- Type of internet connection technologies :
  - Cable: Uses coaxial cables (from TV) to provide internet
  - DSL (Digital Subscriber Line): Uses copper telephone lines for internet
  - Fiber: Uses fiber optic cables for high-speed internet
- Gateway = Modem + Switch + Wifi Router
- NIC (Network Interface Card)
- SDN (Software Defined Networking) : Provides an interface that allows users to manage and control all the network's control planes from a GUI( Abstracting the control plane from the data plane)
- 802.11.ax = WIFI 6
- RFID
- NFC
- 2.4 GHz vs 5GHz , their frequency channels (overlapping?)
- DNS
- DHCP
- proxy
- Load balancer
- IPv4 vs IPv6
- Subnet mask
- Default gateway=ip address of router
- DHCP process = DORA (Design,Offer,Request,Accept)
- APIPA , when there is no DHCP server
- DNS records (Each type of DNS record serves a specific purpose) under DNS configuration:
  - A : Maps a domain name to an IPv4 address.
  - AAAA : Maps a domain name to an IPv6 address
  - CNAME: Aliases one domain name to another
  - MX
- Static DHCP assignment (by MAC address of device)
- DHCP lease renewal
- VLAN (Virtual LAN): Segments a physical network into multiple logical networks (Eg. Use 1 switch instead of 3 switches to make 3 LANs)
- VPN (Virtual Private Network): Eg. Laptop with VPN software enabled -> VPN Concentrator (manages and secures multiple VPN connections) -> Corparate Network
-
