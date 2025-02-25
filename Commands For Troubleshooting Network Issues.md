Commands For Troubleshooting Network Issues
#sre/networking

### NetStat

The `netstat` command is a powerful networking tool used for displaying network connections, routing tables, interface statistics, and more. 

It helps in diagnosing network issues by revealing what ports and services are active, listening, or in use.

what ip addresses are bound or associated to a computer:  
`netstat` : `netstat -in`’

---
**Check Open Ports and Listening Services**
* Helps identify which applications are listening for incoming connections.
* Useful for detecting unauthorized services running on a machine.
* **Example:** 
```bash
netstat -an
```

-a → Show all active connections and listening ports.
-n → Display addresses and ports in numeric format (avoid DNS lookup delays).
---
**Identify Processes Using a Specific Port**
* Helps find which process is using a particular port (useful when an application fails due to port conflicts).
```bash
netstat -ano | findstr :80
```

-o → Show process ID (PID).
findstr :80 → Filters output to show only port 80.
---
**Check Established and Listening Connections**
* Helps diagnose network performance issues or detect unwanted connections.
* **Example:**
```bash
netstat -atn
```

-t → Show TCP connections.
-n → Numeric addresses (no DNS resolution).
---
**Monitor Real-Time Network Connections**
* Helps track incoming and outgoing connections dynamically.
```bash
netstat -c
```

-c → Continuously updates the output.
---
---
### Traceroute

**Traceroute** is a network diagnostic tool used to track the path that data packets take from one computer (or device) to another over a network, such as the internet. It helps identify the route and measure transit delays of packets across an IP network.

##### How Traceroute Works

1) **Sends Packets**: Traceroute sends a series of **ICMP (Internet Control Message Protocol) or UDP packets** to the destination IP address.

2) **Time-To-Live (TTL) Mechanism**: It starts with a TTL value of 1 and increments it by 1 with each subsequent packet.
   * The TTL limits the lifespan of a packet, forcing it to expire at each hop along the route.

3) **Response from Each Hop**:
   * Each router along the way responds with a **"Time Exceeded"** ICMP message, revealing its IP address.
   * The process repeats until the packet reaches its final destination.

4) **Displays Results**: The output shows each hop's IP address, domain name (if resolvable), and round-trip times.

---
Why Use Traceroute?
* **Network Troubleshooting**: Helps diagnose slow connections, high latency, or packet loss.
* **Identifying Network Bottlenecks**: Shows where delays or failures occur in the network path.
* **Checking Routing Paths**: Verifies if traffic is following the expected path.

```bash
traceroute google.com
```
```bash
tracert google.com
```

![](Commands%20For%20Troubleshooting%20Network%20Issues/Screenshot%202025-02-07%20at%206.55.06%E2%80%AFPM.png)

Key Takeaways
✅ **Lower Latency is Better**
* The time should remain relatively low and consistent.
* Higher latency at any hop may indicate network congestion.

⠀✅ **No Timeouts**
* If a hop shows * * * Request Timed Out, it may be a firewall blocking ICMP responses.

⠀✅ **Bottleneck Identification**
* If a specific hop has a sudden, large increase in time, that could indicate a network slowdown.
---
### DIG Command
