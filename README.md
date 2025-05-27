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

# ip地址，Mac地址，接口（Ethernet），端口（port），套接字（socket），程序，网络协议的理解

假设你的设备是一栋办公大楼，ip地址就是你大楼的地址，你可以通过在导航输入这个ip地址，来到办公大楼前。接口就类似于你这个办公楼的整体出入口，可能有前门后门或者等等（可以有多个门）。如果你的办公园区楼很大，每个接口就有自己的地址，你打车到前门和后门是不一样的，但是都是到了这个楼的入口。为了区分，硬件厂家会在出场就为每个接口设置一个MAC地址，是不可以改动的。但你每个接口的ip地址你是可以改动的。你的目的当然不仅仅是来到大楼前，你是要进去办事，所以你进去后，你要和前台交流。前台的工作就类似于操作系统的工作。你要告诉前台，你来这里是想办什么业务（告诉操作系统你的网络协议），找哪个办公室，每个业务部门可能有一个或多个办公室，每个办公室有自己的门牌号，但是一个办公室只能一个业务部门用，这个办公室门牌号就类似于端口号的作用。你还要告诉前台，你找这个业务部门的哪个负责人（哪个程序）。前台接收完你的信息后，就用对讲机给办公室发消息，每个办公室有一台自己的对讲机，套接字就类似于对讲机的工作。


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
RIP：基层算法使用的是Distance Vector
原理：每个Router将自己直接相连的Router的hop count设置为1，然后将这些信息告诉所有和自己直接相连router，同时接收其他直连的router的路由信息，并据此更新自己的路由表，每通过一个设备就将hop count+1，并将最短路径存入。更新后再次发给与自己直连的，直到所有Router的路由表不再更新。超过hop count的设备被定义为不可达，所以更适合小型网络，可以快速收敛。
Each router sets the hop count to 1 for the routers directly connected to it, and then shares this information with all its directly connected routers. At the same time, it receives routing information from its direct neighbors and updates its routing table accordingly. For each additional device passed, the hop count is incremented by 1, and the shortest path is stored. After updating, the router sends the updated information to its directly connected neighbors, and this process continues until the routing tables of all routers no longer change. Devices that exceed the hop count limit are defined as unreachable, making this method more suitable for small networks where it can converge quickly.
OSPF：基层算法是Dijkstra
BGP: Path Vector



