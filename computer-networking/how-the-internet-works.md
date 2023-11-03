# Terminology

| Term        | Description                                                                                                                         |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Packet      | A small unit of data that is transmitted over the internet.                                                                         |
| Router      | A device that directs packets of data between different networks.                                                                   |
| IP Address  | A unique identifier assigned to each device on a network, used to route data to the correct destination.                            |
| Domain Name | A human-readable name that is used to identify a website, such as google.com.                                                       |
| DNS         | The Domain Name System is responsible for translating domain names into IP addresses.                                               |
| HTTP        | The Hypertext Transfer Protocol is used to transfer data between a client (such as a web browser) and a server (such as a website). |
| HTTPS       | An encrypted version of HTTP that is used to provide secure communication between a client and server.                              |
| SSL/TLS     | The Secure Sockets Layer and Transport Layer Security protocols are used to provide secure communication over the internet.         |
| Ports       | Used to identify the application or service running on a device http://example.com:8080/path/to/resource (port is 8080)             |

# How the internet works?

# How a URL Request Works in Computer Networking

- When I enter 'google.com,' my ISP helps me obtain the IP address through the DNS resolution process.
- The DNS resolution process maps the domain name to an IP address.
- An HTTPS request is sent to the IP address server through my ISP using the TCP/IP model.
- The request includes request and response headers with additional information.
- The request is transmitted through the internet backbone, which includes routers, switches, and fiber optic cables.
- Eventually, it reaches Google's servers.
- Google's servers return an HTTPS-encrypted web server response (a secure communication through SSL/TLS encryption used for authentication and secure data transmission).
