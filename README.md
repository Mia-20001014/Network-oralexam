# Network-oralexam
Some basic kownledges in Blatt1

# 经典OSI七层模型每层分别是什么？数据在每一层以什么形式传输？前三层每一层有些什么设备？这些设备的作用是什么？前四层是如何配合的？
The classic OSI 7 layers model: 

1.Physical Layer: Data are stored and trasmitted here as 0 and 1, which is a bitstream.
Devices: cable,repeaters... cable:Transmits bitstreams over physical media; repeaters:Regenerates and amplifies signals to extend transmission range.

2.Data link: Data are encapsulated as a frame in here
Devices: switch, bridges... switch:Forwards frames based on MAC addresses; operates within a LAN. Bridge:Connects two LAN segments; filters traffic based on MAC addresses.

3.Network: Data are encapsulated as a packet in here
Devises：Routers, Firewall. routers: Forwards packets based on IP addresses; connects different networks.

4.Transport:Data are encapsulated as a segment in here
Protocols: TCP,UDP

5.Session
6.Presentation
7.Application

# 网络划分基本结构
subnet和network是第三层的分类，LAN和VLAN是第二层的分类。大多数情况一个LAN包含着一个子网，而同一个LAN中的设备都在地理位置有共同点。一个Network通常由一个或多个LAN来组成。同一个LAN中的设备交流只需要借助switch，同一个network中不同LAN之间的交流需要借助bridge。而不同Network之间的交流是需要借助Router。VLAN是第二层当中一个特殊的LAN，因为通常LAN的划分都是通过地理位置，但如果你想通过一些其他的逻辑来隔离和划分设备的话，你可以把它们接入不同的虚拟LAN中。如果讲同一个网络中位于不同LAN的设备接入同一个VLAN中，它们可以借助该VLAN进行LAN内交流，也就是只通过switch，而不需要bridge。

Subnet and Network are classifications at the third layer, while LAN and VLAN are classifications at the second layer. In most cases, a single LAN contains a single subnet, and the devices within the same LAN typically have a common geographical location. A Network usually consists of one or more LANs. Devices within the same LAN can communicate using a switch, while communication between different LANs within the same Network requires a bridge. Communication between different Networks requires a router.

VLAN is a special type of LAN at the second layer because LANs are usually divided based on geographical locations. However, if you want to isolate and segment devices based on logical criteria, you can place them into different virtual LANs. If devices in different LANs within the same network are connected to the same VLAN, they can communicate with each other as if they are within the same LAN, using only a switch and not a bridge.


# 什么是基于类的地址转发和CIDR？它们的区别是什么？

IPv4 addresses are divided into five classes (A–E) based on their leading bits.
Classes A, B, and C are used for unicast communication; Class D is for multicast, and Class E is reserved.
Each class has its own address range and default subnet mask.
Classful addressing uses the leading bits of an IP address to determine its class and automatically split the address into network and host portions. Routers use this class to forward packets accordingly.
IP Address-->Subnetclass---->Netz_ID-->Next hop

CIDR
IP Address + Router table --> a list of IP Address, which can match the input IP Address --largest prefix match--> Next hop

# 如何探寻一个现有网络的拓扑结构(但还未进行配置)
1. Command: ip address show  ------> check how many ethnets this device have, and each ethnet's ip address(if it has)
3. Command: ip address add 192.168.1.1/24 dev ethX -----> give each ethX on each device a unique IP Address (配置)
4. Command: ip link set ethX up ----->激活每个interface
5. Command: ping -i ethX ------>每个接口去ping另一个指定接口的IP Address，如果可以成功ping，则证明该两设备通过该两接口相连

# tcpdump的基础知识
tcpdump is a network packet capture tool that allows users to intercept and analyze packets on a network. It provides detailed information about each packet passing through a network interface, such as source IP address, destination IP address, protocol type, and port numbers. It's commonly used by network administrators and security analysts to troubleshoot network issues, monitor network traffic, or detect security attacks.
Command:  tcpdump -i <interface> ，默认只显示第三层及以上的info, Option: -e 开启后可以看到第二层的info; -i可以指定看某接口的数据流，否则会捕捉全部 

# ARP and NDP
ARP (Address Resolution Protocol) is used in IPv4 networks to map an IP address to a MAC address. Since communication on the local network happens via MAC addresses, ARP is necessary to discover the hardware address associated with an IP. (like a phone number book)

NDP (Neighbor Discovery Protocol) is used in IPv6 networks and replaces ARP. It provides:
IP-to-MAC address resolution
Stateless address autoconfiguration
Neighbor reachability detection
Router discovery
Prefix distribution

# OSPF,RIP,BGP
OSPF所用算法：Dijkstra
RIP: Distance Vector
BGP: Path Vector



