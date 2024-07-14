# Internet Address Architecture
> Every device connected to the Internet has at least one IP address.

## IPv4 addresses
> IP addresses understand the most popular type

IPv4 address is ==32 bit== in length, which has `4,294,967,296` possible addresses in its address space
```
In [14]: 2**32
Out[14]: 4294967296
```

Such addresses are often represented in so-called `dotted-quad` or `dotted-decimal` notation, for example, `165.195.130.107`. 
The dotted-quad notation consists of four decimal numbers separated by `periods`. 
Each such number (8-bit) is a nonnegative integer in the range `[0, 255]` and represents `one-quarter` of the entire IP address. 

```Python
In [1]: from netaddr import *

In [2]: ip = IPAddress('192.0.1.100')

In [3]: ip.bits()
Out[3]: '11000000.00000000.00000001.01100100'

In [4]: int(ip)
Out[4]: 3221225828

In [5]: int(ip).bit_length()
Out[5]: 32

In [6]: 0b01100100
Out[6]: 100
```

The dotted-quad notation is simply a way of writing the whole  used throughout the Internet system—using convenient decimal numbers. 
![[ipv4_address.png]]
## Classful Addressing

The IPv4 address space was originally divided into five classes. 
Classes A, B, and C were used for assigning addresses to interfaces on the Internet (unicast addresses) and for some other special-case uses. 
The classes are defined by the first few bits in the address: 
- 0 for class A (0-127)
- 10 for class B (128 - 191)
- 110 for class C (192 - 223), 
- and so on. 
Class D addresses are for multicast use
class E addresses remain reserved.

![[ipv4_class.png]]

![[ipv4_class_space_partitioning.png]]
## Subnet Addressing



# The Seven-Layer OSI Model
![[OSI.png]]

Each OSI model layer has a specific function, as follows: 
* Application layer (layer 7)  
The topmost layer of the OSI model provides a means for users to access network resources. This is the only layer typically seen by end users, as it provides the interface that is the base for all of their network activities. 
* Presentation layer (layer 6)  
This layer transforms the data it receives into a format that can be read by the application layer. The data encoding and decoding done here depends on the application layer protocol that is sending or receiving the data. The presentation layer also handles several forms of encryption and decryption used to secure data. 
* Session layer (layer 5)   
This layer manages the dialogue, or session, between two computers. It establishes, manages, and terminates this connection among all communicating devices. The session layer is also responsible for establishing whether a connection is duplex (two-way) or half-duplex (one-way) and for gracefully closing a connection between hosts rather than dropping it abruptly. 
* Transport layer (layer 4)   
The primary purpose of the transport layer is to provide reliable data transport services to lower layers. Through flow control, segmentation/desegmentation, and error control, the transport layer makes sure data gets from point to point error-free. Because ensuring reliable data transportation can be extremely cumbersome, the OSI model devotes an entire layer to it. The transport layer utilizes both connection-oriented and connectionless protocols. Certain firewalls and proxy servers operate at this layer. 
* Network layer (layer 3)   
This layer, one of the most complex of the OSI layers, is responsible for routing data between physical networks. It sees to the logical addressing of network hosts (for example, through an IP address). It also handles splitting data streams into smaller fragments and, in some cases, error detection. Routers operate at this layer. 
* Data link layer (layer 2)   
This layer provides a means of transporting data across a physical network. Its primary purpose is to provide an addressing scheme that can be used to identify physical devices (for example, MAC addresses). Bridges and switches are physical devices that operate at the data link layer. 
* Physical layer (layer 1)   
The layer at the bottom of the OSI model is the physical medium through which network data is transferred. This layer defines the physical and electrical nature of all hardware used, including voltages, hubs, network adapters, repeaters, and cabling specifications. The physical layer establishes and terminates connections, provides a means of sharing communication resources, and converts signals from digital to analog and vice versa. 

## Links
[OSI](https://www.cloudflare.com/en-au/learning/ddos/glossary/open-systems-interconnection-model-osi/)

