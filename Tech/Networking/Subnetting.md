NOTE: while subnets do exist both in IPv4 and IPv6, subnetting is much more important in [IPv4](Subnets%20(IPv4).md) (amongst other reasons due to the smaller overall pool of available addresses)

## Subnet masks
A subnet mask is a 32-bit number, just like any IPv4 address. It allows us to distinguish between the **network portion** and the **host portion** of any IP address. So, if we have an IP address and its subnet mask, we know
1. Which network it belongs to and
2. What the 'local address' of the device within the network is

Furthermore, the subnet mask tells us, how large a subnet could potentially be (i.e. how many local addresses may exist within it at the same time at most).

Just like IP addresses, subnet masks use dotted decimal notation. The most commonly known subnet mask is `255.255.255.0`, as it is used by pretty much any home network's router.

## The history of subnetting
### The 'ancient' approach (before 1981)
At the very beginning, the most significant eight bits (i.e. the first octet) of an IP address defined the _network number_ of any IP and the rest, i.e. the other 24 bits (3 octets), defined the local address of any connected device.

So, for those ancient IP addresses, the first _network number field_ defined the device's  network while the three _rest fields_ uniquely defined the device within the network. As there are 8 bits in the network number field, this resulted in 254 possible networks ($2^8=256$; we need to subtract 2 for the default network `0.0.0.0` and the broadcast address `255.0.0.0`). Within each of those 254 networks, $2^{24}-2=16\,777\,214$ addresses could be assigned to devices (again, $-2$ because the network and broadcast addresses are reserved). Some of those huge networks and their associated numbers were reserved for specific organizations at that time already. A subset of those networks became the known as Class A networks in 1981 when the 'subnetting architecture' was refined further.

### Classful network architecture (1981)
At some point people realized that it's maybe not the best idea to reserve that many addresses to so just a few select organizations. So, they came up with a better system. By the year 1981, (luckily) less than 64 network numbers were assigned. This allowed a reorganization of the current system without breaking any existing architectures. RFC 791 divided the IP address space into 5 classes from A to E:

| Class         | Leading bits | Network number bits | Host identifier bits | Subnet mask    | Address range               |
| ------------- | ------------ | ------------------- | -------------------- | -------------- | --------------------------- |
| A             | 0            | 8                   | 24                   | 255.0.0.0      | 0.0.0.0 - 127.255.255.255   |
| B             | 10           | 16                  | 16                   | 255.255.0.0    | 128.0.0 - 191.255.255.255   |
| C             | 110          | 24                  | 8                    | 255.255.255.0  | 192.0.0.0 - 223.255.255.255 |
| D (multicast) | 1110         | undefined           | undefined            | not applicable | 224.0.0.0 - 239.255.255.255 |
| E (reserved)  | 1111         | undefined           | undefined            | not applicable | 240.0.0.0 - 255.255.255.255 |
Note that the first and last network block within each of the classes A to C (i.e. 0.xxx.xxx.xxx and 127.xxx.xxx.xxx in class A, 128.000.xxx.xxx and 191.255.xxx.xxx in class B, and 192.0.0.xxx and 223.255.255.xxx for class C) were originally reserved and not available for assignment.

## CIDR (1993)
Classless Inter-Domain Routing (CIDR) was introduced after the people responsible for administrating the internet's IP addresses realized that the previous classful network architecture would result in IPv4 addresses being exhausted too quickly. The main issue here was that the three 'IP address classes' from which address ranges (networks) could be assigned (A, B, and C) differed significantly in size and couldn't ever really be used efficiently by any organization. Class A networks were gigantic and not feasible to be used by anyone really, class B networks were still far too big for many enterprises, and class C networks were often too small for larger companies (but still too big for smaller departments of them).