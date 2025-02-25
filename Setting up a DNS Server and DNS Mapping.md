Setting up a DNS Server and DNS Mapping
#sre/networking

[[Domain Name System (DNS)]]

### Creating a Private/Internal Domain (Local Network)

If you want a **private** domain for local use (without registering it on the internet), you can set it up with a **local DNS server**.

Prerequisites: 
1) root/admin access to install and configure DNS
2) a static ip address for your dns server
3) a domain name

#### 1) Create A DNS Server

purpose: allows you to manage my own domain names

##### 1. Setting up a DNS Server on Linux (Using BIND9)
	BIND9 (**Berkeley Internet Name Domain**) is the most widely used DNS server on Linux.

Installing Bind9:
```sh
sudo apt update
sudo apt install bind9 -y   # Ubuntu/Debian
#------------------------------------------------#
sudo yum install bind bind-utils -y # CentOS/RHEL
```

##### 2. Configure Forward Lookup Zone
`forward look up zone` - maps domain names to IP addresses

Edit `BIND` Configuration File:
```sh
sudo nano /etc/bind/named.conf.local
```
```sh
zone "mydomain.local" {
    type master;
    file "/etc/bind/db.mydomain.local";
};
```
Create The File Zone:
```sh
sudo nano /etc/bind/db.mydomain.local
```
```sh

$TTL 86400
@   IN  SOA mydomain.local. admin.mydomain.local. (
        2024020201  ; Serial number
        3600        ; Refresh
        1800        ; Retry
        604800      ; Expire
        86400 )     ; Minimum TTL

@   IN  NS  ns1.mydomain.local.
ns1 IN  A   192.168.1.10
www IN  A   192.168.1.20
```


#### 3) Configure Reverse Lookup Zone
`reverse lookup zone` - maps id address to domain name

Edit `BIND` Configuration File:
```sh
sudo nano /etc/bind/named.conf.local
```
```sh
zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192";
};
```
