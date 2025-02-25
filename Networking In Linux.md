Networking In Linux
#sre/linux #sre/networking

### IP Address (Internet Protocal Address)
`ip adress` (internet protocol address) : is a unique identifier assigned to devices connected to a network, allowing them to communicate with each other

it serves two primary functions: 
1) identification: identifies a device on a network
2) location: specifies the devices location within a network

Types of IP Addresses:
1. IPV4 (Internet Protocol Version 4)
   - 32-bit address, that support about 4.3 billion addresses
2. IPV6 (Internet Protocol Version 6)
   - 128-bit address,  supports an almost unlimited number of addresses

#### Public VS Private IP:
**Public IP**: Assigned by an ISP (Internet Service Provider) and used to communicate over the internet.
**Private IP**: Used within local networks (e.g., home or office) and not routable over the internet (e.g., 192.168.1.1, 10.0.0.1).

#### Static VS Dynamic IP:
* **Static IP**: Fixed and does not change, useful for hosting websites and servers.
* **Dynamic IP**: Assigned temporarily by a DHCP (Dynamic Host Configuration Protocol) server, commonly used by home networks.

#### IP Routing:
Routing Process
1. **Source Device**: When you send a request (e.g., opening a website), your device assigns an IP address to the request and sends it to a **router**.
2. **Router Checks Destination**: Your router looks at the **destination IP address** and determines where to forward the data.
3. **Path Selection (Routing Table)**: Routers use a **routing table** (a list of IP routes) to decide the best path to the destination.
4. **Hops Between Routers**: The data packet is forwarded between multiple routers (hops) until it reaches the target device.
5. **Response Returns**: The server (e.g., the website’s server) sends back data, following a similar route back to your device.

Questions:
1. how can i see how many hops a request is sent to?:
2. what is a port and where do we define it?
3. how can i view packet lost and are there commands / tools to view troubleshooting?

---
### DNS (Domain Name System)

[[Domain Name System (DNS)]]
IP addresses are hard to remember, so we use domain names (like google.com). The **DNS (Domain Name System)** translates these human-friendly names into IP addresses.

#### Domain Name System Components:

- **DNS Resolver** - The client-side service that queries DNS servers to resolve domain names.
- **Root DNS Servers** - Direct queries to top-level domain (TLD) servers (.com, .org, .net, etc.).
- **TLD DNS Servers** - Direct queries to authoritative DNS servers based on domain extensions.
- **Authoritative DNS Servers** - Hold actual domain-to-IP mappings and respond with final answers.

#### How DNS Works:
1. You type google.com into your browser.
2. Your device contacts a **DNS resolver** (usually provided by your ISP or a public service like Google’s 8.8.8.8).
3. The resolver asks **root DNS servers** where to find .com domains.
4. It then queries the **TLD (Top-Level Domain) DNS server** for .com domains.
5. The TLD server directs the request to Google’s **authoritative DNS server**, which returns Google’s IP address (e.g., 142.250.190.46).
6. Your browser connects to that IP, and the website loads.

#### DNS Records:
- **A Record**: Maps a domain to an IPv4 address.
- **AAAA Record**: Maps a domain to an IPv6 address.
- **CNAME Record**: Alias for another domain (e.g., www.example.com → example.com).
- **MX Record**: Used for email routing.
- **PTR Record**: Reverse lookup from IP to domain name.

Questions:
1. how are DNS configured to an IP?:
2. how do we view and configure DNS?:
3. what are some issues that come with DNS for web applications?: