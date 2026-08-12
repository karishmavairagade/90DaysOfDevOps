1. What happens when you type google.com?

The browser asks DNS to resolve google.com into an IP address.
The browser connects to that IP using TCP (for traditional HTTPS) and establishes TLS encryption.
The browser sends an HTTP/HTTPS request to Google’s server.
Google sends the response back, and the browser renders the webpage.

2. DNS record types

A - Maps a domain name to an IPv4 address.
AAAA - Maps a domain name to an IPv6 address.
CNAME - Makes one domain name an alias of another domain name.
MX - Specifies the mail servers responsible for receiving email for a domain.
NS - Specifies the authoritative name servers for a domain.

3. dig google.com

dig google.com

; <<>> DiG 9.20.18-1ubuntu2.1-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 52937
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com.			IN	A

;; ANSWER SECTION:
google.com.		75	IN	A	192.178.211.100
google.com.		75	IN	A	192.178.211.139
google.com.		75	IN	A	192.178.211.138
google.com.		75	IN	A	192.178.211.113
google.com.		75	IN	A	192.178.211.102
google.com.		75	IN	A	192.178.211.101

;; Query time: 64 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Aug 12 23:44:32 IST 2026
;; MSG SIZE  rcvd: 135

****************************************************************************

Task 2: IP Addressing

. What is an IPv4 address?

An IPv4 address is a 32-bit address used to identify a device/interface on an IP network.
It is written as four decimal numbers (octets) separated by dots, each ranging from 0–255.
Example: 192.168.1.10 → four octets: 192 | 168 | 1 | 10.

2. Public vs private IP
Private IP → Used inside a local network and is not directly routable on the public Internet. Example: 192.168.1.10
Public IP → A globally routable address used to communicate over the Internet. Example: 8.8.8.8

3. Private IPv4 ranges

These three ranges are reserved for private networks:
10.0.0.0 – 10.255.255.255	10.0.0.5
172.16.0.0 – 172.31.255.255	172.20.10.5
192.168.0.0 – 192.168.255.255	192.168.1.10

4. Find your private IP with ip addr show

ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp1s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 60:18:95:52:73:90 brd ff:ff:ff:ff:ff:ff
3: wlp0s20f3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 94:e2:3c:ea:02:95 brd ff:ff:ff:ff:ff:ff
    altname wlx94e23cea0295
    inet 192.168.1.46/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s20f3
       valid_lft 84104sec preferred_lft 84104sec
    inet6 2401:4900:881d:ac65:ba4f:8e8b:37f3:2eb1/64 scope global temporary dynamic 
       valid_lft 86064sec preferred_lft 84077sec
    inet6 2401:4900:881d:ac65:8150:ab99:aec:28ee/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 86064sec preferred_lft 86064sec
    inet6 fe80::838c:edc2:b1a8:1909/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 56:e6:21:f0:98:c5 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

*****************************************************************

Task 3: CIDR & Subnetting

1. What does /24 mean?

/24 means 24 of the 32 IPv4 bits are used for the network portion, leaving 8 bits for hosts.
So a /24 contains 2⁸ = 256 total IP addresses.

2. Usable hosts

Formula:

Usable hosts = 2power(host bits) 
/24 - 8 host bits - 254 usable hosts
/16 - 16 host bits - 65,534 usable hosts
/28 - 4 host bits - 14 usable hosts

3. Why do we subnet?

We subnet to divide a large network into smaller, manageable networks.
For eg: a company could have separate subnets for HR, Engineering, and Guests. This makes IP addressing more organized and can improve network performance and security.

4. Fill the table
CIDR	Subnet Mask	Total IPs	Usable Hosts
/24	255.255.255.0	  256		254
/16	255.255.0.0	  65,536	65,534
/28	255.255.255.240	   16		14

****************************************************************************

Task 4: Ports – The Doors to Services

1. What is a port? Why do we need them?

A port is a 16-bit number used to identify a specific network service or application on a device.

Think of an IP address as the building address and a port as the apartment/office number.
For eg:(IP)192.168.1.10:443( Port)
The IP tells the network which machine to reach; the port tells it which service/application should receive the traffic.

2. Common ports
Port	Service
22	SSH — secure remote login
80	HTTP — unencrypted web traffic
443	HTTPS — encrypted web traffic
53	DNS — domain-name resolution
3306	MySQL
6379	Redis
27017	MongoDB

3. ss -tunlp

ss -tunlp
Netid       State        Recv-Q       Send-Q                                     Local Address:Port                Peer Address:Port       Process                                    
udp         UNCONN       0            0                                                0.0.0.0:5353                     0.0.0.0:*           users:(("firefox",pid=5853,fd=273))       
udp         UNCONN       0            0                                                0.0.0.0:5353                     0.0.0.0:*                                                     
udp         UNCONN       0            0                                             127.0.0.54:53                       0.0.0.0:*                                                     
udp         UNCONN       0            0                                          127.0.0.53%lo:53                       0.0.0.0:*                                                     
udp         UNCONN       0            0                                              127.0.0.1:323                      0.0.0.0:*                                                     
udp         UNCONN       0            0                                                0.0.0.0:51433                    0.0.0.0:*           users:(("python3",pid=14047,fd=9))        
udp         UNCONN       0            0                                                0.0.0.0:52413                    0.0.0.0:*           users:(("python3",pid=14047,fd=12))       
udp         UNCONN       0            0                                           192.168.1.46:3702                     0.0.0.0:*           users:(("python3",pid=14047,fd=10))       
udp         UNCONN       0            0                                        239.255.255.250:3702                     0.0.0.0:*           users:(("python3",pid=14047,fd=8))        
udp         UNCONN       0            0                                             172.17.0.1:3702                     0.0.0.0:*           users:(("python3",pid=14047,fd=13))       
udp         UNCONN       0            0                                        239.255.255.250:3702                     0.0.0.0:*           users:(("python3",pid=14047,fd=11))       
udp         UNCONN       0            0                                                   [::]:5353                        [::]:*                                                     
udp         UNCONN       0            0                                                      *:46474                          *:*           users:(("firefox",pid=5853,fd=179))       
udp         UNCONN       0            0                                                  [::1]:323                         [::]:*                                                     
udp         UNCONN       0            0                  [fe80::838c:edc2:b1a8:1909]%wlp0s20f3:546                         [::]:*                                                     
udp         UNCONN       0            0                                                      *:58177                          *:*           users:(("firefox",pid=5853,fd=190))       
udp         UNCONN       0            0                                                      *:50371                          *:*           users:(("python3",pid=14047,fd=15))       
udp         UNCONN       0            0                                                      *:34847                          *:*           users:(("firefox",pid=5853,fd=128))       
udp         UNCONN       0            0                  [fe80::838c:edc2:b1a8:1909]%wlp0s20f3:3702                        [::]:*           users:(("python3",pid=14047,fd=16))       
udp         UNCONN       0            0                                    [ff02::c]%wlp0s20f3:3702                        [::]:*           users:(("python3",pid=14047,fd=14))       
udp         UNCONN       0            0                                                      *:45973                          *:*           users:(("firefox",pid=5853,fd=184))       
tcp         LISTEN       0            4096                                          127.0.0.54:53                       0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                           127.0.0.1:42351                    0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                           127.0.0.1:631                      0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                       127.0.0.53%lo:53                       0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                               [::1]:631                         [::]:*                                                     

******************************************************************
Task 5: Putting It Together

1. You run curl http://myapp.com:8080 — what networking concepts from today are involved?

curl http://myapp.com:8080 - DNS resolves myapp.com to an IP, then TCP connects to port 8080, and HTTP sends the request. This involves DNS - IP - TCP - port - HTTP.

2. Your app can't reach a database at 10.0.1.50:3306 — what would you check first?

First check basic network connectivity/routing to 10.0.1.50, then check whether port 3306 is reachable/listening. Also verify the database service is running and that firewall/security rules allow the connection.
