# [Classless Inter-Domain Routing (CIDR)](https://aws.amazon.com/what-is/cidr/)

CIDR is an IP address allocation method that improves data routing efficiency on the internet. Every machine, server, and end-user device that connetcs to the internet has a unique number, called an IP address, associated with it. Devices find and communicate with one another by using these IP addresses. Organizations use CIDR to allocate IP addresses flexibly and efficiently in their networks.

## What are the different IP address formats?

An IP address has two parts:

* The *network address* is a series of numerical digits pointing to the network's unique identifier.

* The *host address* is a series of numbers indicating the host or individual device identifier on the network.

Until the early 1990s, IP addresses were allocated using the classful addressing system. The total length of the address was fixed, and the number of bits allocated to the network and host portions were also fixed.

### Classful addresses

An IPv4 address consists of 32 bits. Each string of numbers separated by the period consists of 8 bits, represented by 0 to 255 in numerical forms. Organizations could purchase three classes of IPv4 addresses.

*Class A*  

A Class A IPv4 address has 8 network prefix bits. For example, consider 44.0.0.1, where 44 is the network address and 0.0.1 is the host address.

*Class B*

A Class B IPv4 address has 16 network prefix bits. For example, consider 128.16.0.2, where 128.16 is the network address and 0.2 is the host address.

*Class C*

A Class C IPv4 address has 24 network prefix bits. For instance, consider 192.168.1.100, where 192.168.1 is the network address and 100 is the host address.

### Classless addresses

Classes or Classless Inter-Domain Routing (CIDR) addresses use variable length subnet masking (VLSM) to alter the ratio between the network and host address bits in an IP address. A subnet mask is a set of identifiers that returns the network address's value from the IP address by turning the host address into zeros.

A VLSM sequence allows network administrators to break down an IP address space into subnets of various sizes. Each subnet can have a flexible host count and a limited number of IP addresses. A CIDR IP address appends a suffix value stating the number of network address prefix bits toa  noraml IP address.

For example, 192.0.2.0/24 is an IPv4 CIDR address where the first 24 bits, or 192.0.2, is the network address.

## What are the limitations of classful IP addressing that CIDR overcomes?

Before Classless Inter-Domain Routing (CIDR), IP addresses were classful and created inefficiencies. We discuss some of these shortcomings next.

**Inflexible IP addressing**  

In a classful addressing system, each class supported a fiexed number of devices:

* Class A supported 16,777,214 hosts

* Class B supported 65,534 hosts

* Class C supported 254 hosts

The classful arrangement was inefficient when allocating IP addresses and led to a waste of IP address spaces.

For example, an organization with 300 devices couldn't have used a Class C IP address, which only permitted 254 devices. So, the organization would've been forced to apply for a Class B IP address, which provided 65,534 unique host addresses. However, only 300 devices would've been connected, which would've left 65,234 unused IP address spaces.

**Limitations in network design**

Classful IPs limited your ability to combine networks as required. For example, these IP addresses belong to different class C networks in the classful architecture:

* 192.168.1.0
* 192.168.0.0

As a network administrator, you couldn't have combined both networks because the class C subnet mask was fixed as 255.255.255.0.

## What are the benefits of CIDR?

With Classless Inter-Domain Routing (CIDR), your organization has more flexibility in assigning IP addresses and routing data between devices.

**Reduce IP address wastage**

CIDR provides flexibility when you determine the network and host identifier assignments on an IP address. You can use CIDR to provision the required number of IP addresses for a particular network and reduce wastage. Besides, CIDR reduces routing table entries and simplifies data packet routing.

**Transmit data quickly**

CIDR allows routers to organize IP addresses into multiple subnets more efficiently. A subnet is a smaller network that exists within a network. For example, all devices connected to a router are on the same subnet and have the same IP address prefix.

With CIDR, your organization can create and consolidate multiple subnets. This allows data to reach the destination address without taking unnecessary paths.

**Create a Virtual Private Cloud**

A virtual private cloud (VPC) is a private digital space hosted within the cloud. It allows your organization to provision workloads in an isolated and secure environment. A VPC uses CIDR IP addresses when it transfers data packets between connected devices.

**Create supernets flexibly**

A supernet is a group of subnets with similar network prefixes. CIDR allows flexibility in creating supernets, which isn't possible in conventional masking architecture. For example, your organization can combine IP addresses into a single network block using a notation like this:

* `192.168.1 /23`
* `192.168.0 /23`

This notation applies a subnet mask of `255.255.254.0` to the IP address, which returns the first 23 bits as the network address. The router needs only one routing table entry to manage data packets between devices on the subnets.

## How does CIDR work?

Classless Inter-Domain Routing (CIDR) allows network routers to route data packets to the respective device based on the indicated subnet. Instead of classifying the IP address based on classes, router retrieve the network and host address as specified by the CIDR suffix.

It's important to understand CIDR blocks and CIDR notation to learn how CIDR works.

**CIDR blocks**

A CIDR block is a collection of IP addresses that share the same network prefix and number of bits. A large block consists of more IP addresses and a small suffix.

The Internet Assigned Numbers Authority (IANA) assigns large CIDR blocks to regional internet registries (RIR). Then, the RIR assigns smaller blocks to local internet registries (LIR), which then assign them to organizations. Meanwhile, private users apply for CIDR blocks from their internet service providers.

* **Master CIDR Block:** `10.10.0.0/16`
    * **Subnet 1:** `10.10.1.0/24`
    * **Subnet 2:** `10.10.2.0/24`
    * **Subnet 3:** `10.10.3.0/24`
    * **Subnet 4:** `10.10.4.0/24`
    * **Subnet 5:** `10.10.5.0/24`

**CIDR notation**  

CIDR notation represents an IP address and a suffix that indicates network identifier bits in a specified format. For example, you could express `192.168.1.0` with a 22-bit network identifier as `192.168.1.0/22`.

## How is CIDR used in IPv6?

IPv6 is a network addressing system designed to replace IPv4. IPv6 uses a 128-bit unique identifier, which allows it to hold 1,028 times more IP addresses than IPv4.

An IPv6 address consists of 8 colon-separated hexadecimal values. IPv6 allows a much larger address space to accommodate the increasing number of devices that are connecting to the internet today.

Under Classless Inter-Domain Routing (CIDR), IPv6 addresses can be aggregated with prefixes of arbitrary bit length, similar to IPv4 addresses. For example, `2001:0db8:/32` is an IPv6 CIDR address, with the first 32 bits, or `2001:db8`, as the network address.

## Bit Conversions

Given 8 bits (an octect):

Bit Place: | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 
-----------|---|---|---|---|---|---|---|--
**Set Value:** | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1

```
0000 0001 = 1
0000 0010 = 2
1000 0000 = 128
0000 0011 = 3
1100 0000 = 192
1111 1111 = 255
```

`10.12.10.0/22`

```
# 22 Bit CIDR
1111 1111.1111 1111.1111 1100.0000 0000
Subnet Mask:   255.255.252.0
Wildcard Mask: 0.0.3.255

# Decimal
10.12.10.0

# Binary
0000 1010.0000 1100.0000 1010.0000 0000

# 22 Bit CIDR
1111 1111.1111 1111.1111 1100.0000 0000
```

The bits in the subnet mask set to `1` identify the network address, or the bits in the subnet that will not change.

The bits in the subnet mask set to `0` identify the host address, or the bits in the subnet that can vary.

```
# Variation on 3rd Octet
1111 1100

# Default Subnet 3rd Octect
0000 1010

# Lowest Subnet 3rd Octet
0000 1000 = 8

# Highest Subnet 3rd Octet
0000 1011 = 11
```

**Range:** 10.12.8.0 - 10.12.11.255

