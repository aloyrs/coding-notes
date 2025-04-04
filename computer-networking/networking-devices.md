# Networking devices

| **Network Device** | **TCP/IP Model Layer** | **Common Uses** | Comments |
| --- | --- | --- | --- |
| Hub | Physical Layer | Hubs receive incoming data signals from one port and then broadcast them to all other ports | Bad , inefficient use of bandwidth |
| Repeater | Physical Layer | Extend the range of a network |  |
| Bridge | Data Link Layer | Connect separate network segments together |  |
| Switch | Data Link Layer | Connect devices within a network | Layer 2 device , stores and uses MAC addresses in CAM (Content Addressable Memory) table |
| Router | Network Layer | Connect separate networks and route traffic between them |  |
| Firewall | Network Layer / Transport Layer | Protect a network from unauthorized access |  |
| Load Balancer | Transport Layer / Application Layer | Distribute traffic across multiple servers to improve performance and reliability |  |
| Proxy Server | Application Layer | Control and manage access to the Internet |  |
| Gateway | Various Layers, depending on function and placement in network | Connect separate networks with different protocols or technologies |  |

- Hub: A hub is a simple device that operates at the physical layer of the TCP/IP model. Its main function is to connect multiple devices (such as computers, printers, and servers) to a network. Hubs receive incoming data signals from one port and then broadcast them to all other ports, which can lead to network congestion and collisions.
- Repeater: A repeater is also a device that operates at the physical layer of the TCP/IP model. Its main purpose is to extend the range of a network by amplifying and regenerating signals. A repeater receives a weak or degraded signal from one network segment and then transmits it with renewed strength to another segment.
- Bridge: A bridge is a device that operates at the data link layer of the TCP/IP model. Its primary function is to connect two separate network segments together and manage the flow of data between them. A bridge can filter and forward incoming data frames based on their MAC addresses, which helps to reduce network traffic and improve performance.
- Switch: A switch is a device that operates at the data link layer of the TCP/IP model. It is similar to a bridge, but with more advanced features and capabilities. A switch can connect devices within a local area network (LAN) and use MAC addresses to forward data packets only to the intended recipient. This results in faster and more efficient data transmission than with a hub.
- Router: A router is a device that operates at the network layer of the TCP/IP model. Its main function is to connect separate networks (such as LANs, WANs, and the Internet) and route traffic between them. A router uses IP addresses to identify and direct packets of data to their destination, which enables communication between devices on different networks.
- Firewall: A firewall is a network security device that can operate at the network layer and/or transport layer of the TCP/IP model. Its primary function is to protect a network from unauthorized access, by filtering incoming and outgoing traffic based on pre-defined rules and policies. A firewall can help to prevent hacking, malware infections, and other cyber threats.
- Load Balancer: A load balancer is a device that operates at the transport layer and/or application layer of the TCP/IP model. Its main purpose is to distribute network traffic across multiple servers, in order to optimize performance, availability, and scalability. A load balancer can help to prevent server overload, downtime, and slow response times, by evenly spreading the workload among servers.
- Proxy Server: A proxy server is a device that operates at the application layer of the TCP/IP model. Its main function is to control and manage access to the Internet, by acting as an intermediary between client devices and web servers. A proxy server can help to improve security, privacy, and performance, by caching frequently accessed web content, filtering incoming traffic, and masking client IP addresses.
- Gateway: A gateway is a versatile network device that can operate at various layers of the TCP/IP model, depending on its function and placement in the network. Generally, a gateway is used to connect separate networks that use different protocols or technologies, and to facilitate data exchange between them. For example, a network gateway can enable communication between a LAN and a cloud-based service, or between a wired network and a wireless network.

[](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%2738%27%20height=%2738%27/%3e)