# Terminology

| Term        | Description                                                                                                                                                                                                                           |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Packet      | A small unit of data that is transmitted over the internet.                                                                                                                                                                           |
| Router      | A device that directs packets of data between different networks.                                                                                                                                                                     |
| IP Address  | A unique identifier assigned to each device on a network, used to route data to the correct destination.                                                                                                                              |
| Domain Name | A human-readable name that is used to identify a website, such as google.com.                                                                                                                                                         |
| DNS         | The Domain Name System is responsible for translating domain names into IP addresses.                                                                                                                                                 |
| URL         | Uniform Resource Locator ,sometimes called a web address , eg. ‘https://cloudflare.com/learning/’ ,‘cloudflare.com’ is the domain name, while ‘https’ is the protocol and ‘/learning/’ is the path to a specific page on the website. |
| HTTP        | The Hypertext Transfer Protocol is a TCP/IP based protocol used to transfer data between a client (such as a web browser) and a server (such as a website).                                                                           |
| HTTPS       | An encrypted version of HTTP that is used to provide secure communication between a client and server.                                                                                                                                |
| SSL/TLS     | The Secure Sockets Layer and Transport Layer Security protocols are used to provide secure communication over the internet.                                                                                                           |
| Ports       | Used to identify the application or service running on a device http://example.com:8080/path/to/resource (port is 8080)                                                                                                               |

# How the internet works?

# How a URL Request Works in Computer Networking

- When I enter 'google.com' into my browser, my ISP (Internet Service Provider) helps me obtain the IP address through the DNS resolution process.
- The DNS resolution process maps the domain name to an IP address, allowing my computer to know where to send the request.
- An HTTPS request is sent from my computer to the IP address. Before it leaves my house, the data passes through my home router.
- My home router manages the local network and directs the request to the home modem.
- The request, including request and response headers with additional information, is then transmitted from my home modem through my ISP using the TCP/IP model.
- Once at the ISP, the request is routed through the internet backbone, which includes routers, switches, and fiber optic cables.
- Eventually, the request reaches Google's servers.
- Google's servers return an HTTPS-encrypted web server response (a secure communication through SSL/TLS encryption used for authentication and secure data transmission).
- The response follows the reverse path, passing through routers, switches, and eventually reaching my home modem and router, and then my computer, to be displayed in the browser.

This process highlights the role of the home modem and router in directing local network traffic and the subsequent journey through the internet to access a website.
