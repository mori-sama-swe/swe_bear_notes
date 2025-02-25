Domain Name System (DNS)
#sre/networking

The `Domain Name System` : translates **human-readable domain names** (e.g., www.google.com) into **IP addresses** (e.g., 142.250.191.78) that computers use to identify each other on a network. 
This process allows users to access websites using easily memorable names instead of complex numerical IP addresses.

what is an IP Address : [[IP Addresses (Internet Protocol Address)]]

#### What Does Domain Name Systems Do?:
key functions:
1. translates domain names into ip addresses: This allows devices to locate and communicate with servers hosting websites and services.

2. provides redudency and fault tolerance: If one DNS server fails, another can take over to keep the internet functioning smoothly.

(question) How do I know if a DNS is failing and how can they fail?: 

#### Components of Domain Name Systems:

1. **DNS Resolver (Recursive Resolver):** the first stop is a DNS query, the `resolver` is responsible for taking a users request and searching for the corressponding `IP Address`
   - it either finds the IP in its cache or queries other `DNS Servers`

2. **Root DNS Server:** direct requests to the appropriate (Top-Level Domain Server)

3. **TLD (Top-Level Domain) Server:** stores information about domain extensions (.com,.org,.net)

4. **Authoritative DNS Server:** the final stop in the DNS lookup process, contains the actual IP Address mapping for the domain : MANAGED by website owners and hosting providers

(question) How do route / map a DNS to an IP?
(question) How do i set-up a DNS Server?

---

#### DNS Resolution Path ( How A Domain Name Is Resolved)

When you type www.example.com into your browser, the DNS resolution process follows these steps:

Step 1: User Requests a Website
* A user enters www.example.com into a web browser.

Step 2: Query Sent to the Recursive Resolver
* The request is sent to a **DNS resolver** (typically managed by your ISP or a third-party service like Google DNS or Cloudflare).

Step 3: Recursive Resolver Checks Cache
* If the resolver has a cached response for www.example.com, it returns the IP address.
* If not, it queries the Root DNS Server.

Step 4: Root DNS Server Responds
* The root server doesn’t know the IP of www.example.com, but it directs the request to the appropriate TLD server (e.g., .com TLD).

Step 5: TLD DNS Server Responds
* The TLD server looks up example.com and directs the resolver to the **authoritative DNS server**.

Step 6: Authoritative DNS Server Responds
* The authoritative server contains the IP address for www.example.com and sends it to the resolver.

Step 7: Resolver Sends the IP Address to the Browser
* The recursive resolver returns the IP (192.0.2.1, for example) to the user's browser.

Step 8: Browser Connects to the Website
* The browser uses the retrieved IP address to connect to the web server and load the website.
---
#### Managing and Troubleshooting DNS Issues

1. nslookup - name server lookup
Used to query DNS records and resolve domain names to IP addresses.
```bash
nslookup google.com
```
output ex:
```bash
Server:  8.8.8.8                # DNS resolver being used (Google Public DNS in this case)
Address: 8.8.8.8

Non-authoritative answer:        # Not from the root or authoritative DNS server
Name:    google.com              # The domain name queried
Address: 142.250.191.46          # The resolved IP address
```

2. host (simple dns lookup)
a command similar to `nslookup` but available for macOs
```bash
host google.com
```
output ex:
```
google.com has address 142.250.191.46  # IPv4 address
google.com has IPv6 address 2607:f8b0:4007:80b::200e  # IPv6 address
```

3. traceroute (track DNS path)
Shows the path packets take to reach a destination.
```bash
traceroute google.com  # Linux/macOS
tracert google.com     # Windows
```
output:
```bash
1  192.168.1.1 (Router)
2  10.0.0.1 (ISP Gateway)
3  142.250.191.46 (Google Server)  # Destination reached
```
