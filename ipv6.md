# [IPv6](https://www.linkedin.com/advice/0/how-do-you-subnet-ipv6-addresses-what-differences)

IPv6 addresses are 128 bits long, compared to 32 bits for IPv4 addresses. The basic structure of an IPv6 address is composed of two parts: a 64-bit network prefix and a 64-bit interface identifier. The network prefix identifies the subnet, while the interface identifier identifies the device within the subnet. The network prefix can be further divided into a global routing prefix, a subnet ID, and a site prefix, depending on the scope and hierarchy of the network. The interface identifier can be derived from the MAC address of the device or generated randomly.

## IPv6 Subnets

To subnet an IPv6 address, you need to determine the length of the network prefix and the subnet mask. The network prefix length is the number of bits that are fixed in the address, while the subnet mask is a binary pattern that indicates which bits are part of the network prefix and which bits are part of the interface identifier. The network prefix length and the subnet mask are usually written in slash notation, such as `/64` or `/48`.

For example, if you have an IPv6 address of `2001:db8:abcd:1234::1/64`, it means that the network prefix is `2001:db8:abcd:1234` and the interface identifier is `::1`. The subnet mask is 64 bits of 1s followed by 64 bits of 0s. To create subnets, you can borrow bits from teh interface identifier and add them to the network prefix. For instance, if you want to create four subnets, you can borrow two bits from the interface identifier and assign them different values, such as 00, 01, 10, and 11. this will create four subnets with network prefixes of:
* `2001:db8:abcd:1234:0::/66`
* `2001:db8:abcd:1234:4000::/66`
* `2001:db8:abcd:1234:8000::/66`
* `2001:db8:abcd:1234:c000::/66`

## How to Calculate IPv6 Subnets

To calculate the number of subnets and hosts that can be created from an IPv6 address, you can use the following formulas:

The number of subnets equals 2 to the power of (*n* minus *m*), where *n* is the network prefix length and *m* is the original network prefix length.

The number of hosts per subnet equals 2 to the power of (128 minus *n*) where *n* is the network prefix length.

For example, if you have an IPv6 address of `2001:db8:abcd:1234::1/64` and you want to create foru subnets with `/66` network prefixes, you can use the formulas as follows:

2 to the power of (66 minus 64) = 2^2 = 4

2 to the power of (128 minus 66) = 2^62 = 4,611,686,018,427,387,904

> The above number is a staggering 4 quintillion, 611 quadrillion, 686 trillion, 18 billion, 427 million, 287 thousand, 904 hosts. See [Number Scale](./number-scale.md).

## How to Write IPv6 Subnets

When writing IPv6 subnets, you should adhere to certain rules and conventions. These include using hexadecimal digits (0-9 and A-F) to represent each group of four bits in the address, separating each group of 16 bits with colons (:), replacing consecutive groups of zeros with double colons (::), and using lowercase letters for hexadecimal digits. Additonally, you should use slash notation (/) to indicate the network prefix length or subnet mask.

Full Form | Compressed Form
----------|----------------
`2001:db8:abcd:1234:c000:0000:0000:0000/66` | `2001:db8:abcd:1234:c00::/66`

## Differences from IPv4 Subnetting

IPv6 subnetting has some differences from IPv4 subnetting, such as longer and more complex addresses using hexadecimal digits separated by colons, and double colons to compress the address. Additionally, IPv6 addresses have a fixed network prefix length of 64 bits, while IPv4 addresses can have variable network prefix lengths. Furthermore, IPv6 addresses provide a larger number of subnets and hosts than IPv4 addresses.