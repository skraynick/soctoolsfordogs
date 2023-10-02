![[Pasted image 20231001185400.png]]
##  Arp scan.
### Indicators
- During ARP scanning, an attacker is typically sending a large number of ARP requests on the broadcast (ff:ff:ff:ff:ff:ff) destined to the MAC address 00:00:00:00:00:00 in order to discover alive IP addresses on the local network. We will typically see something like this:

```
Who has 192.168.0.1? Tell 192.168.0.53
Who has 192.168.0.2? Tell 192.168.0.53
Who has 192.168.0.3? Tell 192.168.0.53
Who has 192.168.0.4? Tell 192.168.0.53
Who has 192.168.0.5? Tell 192.168.0.53
```

Times of packets will be tight and IPS will be changing, often sequential. 

#### Wireshark filter

```
arp.dst.hw_mac==00:00:00:00:00:00
```


## IP Protocol Scan
### Indicators
How ICMP ping sweeping looks like in Wireshark:
![[Pasted image 20231001184032.png]]

If we see too many of these packets in a short period of time targeting many different IP addresses, then we are probably witnessing ICMP ping sweeps. Someone is trying to identify all alive IP addresses on our network (e.g. by running `nmap -sn -PE <subnet>` ).
#### Wireshark Filter
```
icmp.type==3 and icmp.code==2
```

## TCP ping sweeps
### Indicators
![[Pasted image 20231001184238.png]]

TCP ping sweeps typically use port 7 (echo). If we see a higher volume of such traffic destined to many different IP addresses, it means somebody is probably performing TCP ping sweeping to find alive hosts on the network (e.g. by running `nmap -sn -PS/-PA <subnet>` ).

#### Wireshark Filter
```
tcp.dstport==7
```


## UDP ping Sweeps
### Indicators
![[Pasted image 20231001185254.png]]

Similarly as TCP, UDP ping sweeps typically utilize port 7 (echo). If we see a high volume of such traffic destined to many different IP addresses, it means somebody is probably performing UDP ping sweeping to find alive hosts on the network (e.g. by running `nmap -sn -PU <subnet>` ).

## TCP SYN

### Indicators
![[Pasted image 20231001185814.png]]

- SYN flag set
- ACK flag not set
- Window size <= 1024 bytes

This is basically a first step in the TCP [3-way handshake](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/) (the beginning of any TCP connection), with a very small TCP window size.

The small window size in particular is the characteristic parameter used by tools such as nmap or massscan during SYN scans, indicating that there will be essentially very little or no data.

If we see too many packets of this kind in a short period of time, someone is most likely doing:

- SYN scans in our network (e.g. by running `nmap -sS <target>` )
- SYN port sweeps across the network (e.g. by running `nmap -sS -pXX <subnet>` )
- SYN floods (denial of service technique)

### Wireshark Command
```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024
```


## TCP Xmass scan

### Indicators
![[Pasted image 20231001190052.png]]

TCP Xmass scan work by sending packets with FIN, PUSH and URG flags set. This is yet another technique of penetrating some of the firewalls to discover open ports.

If we see such packets in our network, someone is probably performing TCP Xmass scans (e.g. by running `nmap -sX <target>` ).
#### Wireshark Command
```
tcp.flags.fin==1 && tcp.flags.push==1 && tcp.flags.urg==1
```



![[Pasted image 20231001190257.png]]

## ARP poisoning
### Indicators
This filter will display any occurrence of a single IP address being claimed by more than one MAC address. Such situation likely indicates that ARP poisoning is happening in our network.

ARP poisoning (also known as ARP spoofing) is a technique used to intercept network traffic between the router and other clients on the local network. It allows the attacker to perform man-in-the-middle (MitM) attacks on neigboring computers on the local network using tools such as [arpspoof](https://github.com/tecknicaltom/dsniff), [ettercap](https://github.com/Ettercap/ettercap) and others.

#### Wireshark Filter
```
arp.duplicate-address-detected or arp.duplicate-address-frame
```

SOURCE: https://www.infosecmatter.com/detecting-network-attacks-with-wireshark/

https://www.hackingarticles.in/understanding-nmap-scan-wireshark/

|   |   |
|---|---|
|!(ip.src == 162.248.16.53)|Shows all packets except those originating from 162.248.16.53|ter