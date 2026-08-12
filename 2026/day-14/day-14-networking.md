1. OSI layers (L1–L7) vs TCP/IP stack (Link, Internet, Transport, Application)

OSI (7 layers)	TCP/IP (4 layers)

L7 Application  
L6 Presentation    Application
L5 Session  

L4 Transport       Transport

L3 Network        Internet

L2 Data Link     
L1 Physical           Link


2. Where IP, TCP/UDP, HTTP/HTTPS, DNS sit in the stack

IP → Internet layer (OSI L3)
Handles addressing and routing packets.
TCP / UDP → Transport layer (OSI L4)
TCP: reliable, connection-oriented delivery.
UDP: lightweight, connectionless delivery.
HTTP / HTTPS → Application layer (OSI L7)
HTTP transfers web requests/responses.
HTTPS is HTTP protected with TLS.
DNS → Application layer (OSI L7)
Converts names such as example.com into IP addresses.
DNS commonly uses UDP, but can also use TCP.

Application - http, https  & DNS
Transport - TCP and UDP
Internet - Ip
Link - Ethernet & wifi

3. One real example: “curl https://example.com = App layer over TCP over IP”

karishma@MyPc:~$ curl https://example.com
<!doctype html><html lang="en"><head><title>Example Domain</title><link rel="icon" href="data:,"><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style></head><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p><p><a href="https://iana.org/domains/example">Learn more</a></p></div></body></html>
karishma@MyPc:~$ 

****************************************************************************************

Hands-on Checklist 

1. Identify (hostname -I/ip addr)
karishma@MyPc:~$ hostname -I 
192.168.1.46 172.17.0.1 2401:4900:881d:ac65:ba4f:8e8b:37f3:2eb1 2401:4900:881d:ac65:8150:ab99:aec:28ee 
karishma@MyPc:~$ ip addr 
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
       valid_lft 84845sec preferred_lft 84845sec
    inet6 2401:4900:881d:ac65:ba4f:8e8b:37f3:2eb1/64 scope global temporary dynamic 
       valid_lft 85963sec preferred_lft 84818sec
    inet6 2401:4900:881d:ac65:8150:ab99:aec:28ee/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 85963sec preferred_lft 85963sec
    inet6 fe80::838c:edc2:b1a8:1909/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 56:e6:21:f0:98:c5 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
karishma@MyPc:~$ 

2. Ping

karishma@MyPc:~$ ping google.com
PING google.com (2404:6800:4009:806::200e) 56 data bytes
64 bytes from pnbomb-ad-in-x0e.1e100.net (2404:6800:4009:806::200e): icmp_seq=1 ttl=117 time=21.5 ms
64 bytes from pnbomb-ad-in-x0e.1e100.net (2404:6800:4009:806::200e): icmp_seq=2 ttl=117 time=21.0 ms
64 bytes from pnbomb-ad-in-x0e.1e100.net (2404:6800:4009:806::200e): icmp_seq=3 ttl=117 time=27.2 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 21.012/23.229/27.213/2.823 ms

3. TRACEROUTE

karishma@MyPc:~$ traceroute google.com
traceroute to google.com (2404:6800:4009:806::200e), 30 hops max, 80 byte packets
 1  2401:4900:881d:ac65::1 (2401:4900:881d:ac65::1)  2.194 ms  2.145 ms  2.123 ms
 2  * * *
 3  fc00::b2 (fc00::b2)  14.883 ms fc00::b3 (fc00::b3)  14.130 ms fc00::9a (fc00::9a)  15.345 ms
 4  2404:a800:2a00:102::51 (2404:a800:2a00:102::51)  8.456 ms  8.402 ms 2404:a800:2a00:102::4d (2404:a800:2a00:102::4d)  38.783 ms
 5  * * *
 6  2404:a800::167 (2404:a800::167)  21.455 ms  23.033 ms  19.275 ms
 7  2001:4860:1:1::3900 (2001:4860:1:1::3900)  19.137 ms  19.044 ms  22.780 ms
 8  2001:4860:0:1::7965 (2001:4860:0:1::7965)  21.681 ms 2001:4860:0:1::87f3 (2001:4860:0:1::87f3)  21.624 ms  24.509 ms
 9  2001:4860:0:1::7ba9 (2001:4860:0:1::7ba9)  23.294 ms  21.380 ms 2001:4860:0:1::7ba7 (2001:4860:0:1::7ba7)  17.931 ms
10  pnbomb-ad-in-x0e.1e100.net (2404:6800:4009:806::200e)  18.278 ms  22.976 ms  20.995 ms

4. ss -tunlp
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
udp         UNCONN       0            0                                                  [::1]:323                         [::]:*                                                     
udp         UNCONN       0            0                  [fe80::838c:edc2:b1a8:1909]%wlp0s20f3:546                         [::]:*                                                     
udp         UNCONN       0            0                                                      *:50371                          *:*           users:(("python3",pid=14047,fd=15))       
udp         UNCONN       0            0                                                      *:34847                          *:*           users:(("firefox",pid=5853,fd=128))       
udp         UNCONN       0            0                  [fe80::838c:edc2:b1a8:1909]%wlp0s20f3:3702                        [::]:*           users:(("python3",pid=14047,fd=16))       
udp         UNCONN       0            0                                    [ff02::c]%wlp0s20f3:3702                        [::]:*           users:(("python3",pid=14047,fd=14))       
tcp         LISTEN       0            4096                                          127.0.0.54:53                       0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                           127.0.0.1:42351                    0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                           127.0.0.1:631                      0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                       127.0.0.53%lo:53                       0.0.0.0:*                                                     
tcp         LISTEN       0            4096                                               [::1]:631                         [::]:*                                                     


5. DIG

dig google.com

; <<>> DiG 9.20.18-1ubuntu2.1-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 57232
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com.			IN	A

;; ANSWER SECTION:
google.com.		133	IN	A	142.250.71.110

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Aug 12 23:38:32 IST 2026
;; MSG SIZE  rcvd: 55

6. NETSTAT

netstat -an | head -n 3
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN     


