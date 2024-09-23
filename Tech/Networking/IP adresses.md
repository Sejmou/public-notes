### Standards
### IPv4
IPv4 address are 32 bits large. Logically, those 32 bits are split into 4 consecutive octets. 1 octet therefore consists 8 bits, which is equivalent to 1 byte in most, but not all cases (bytes aren't _always_ 8 bits long, this depends on the processor architecture).

To make the IP addresses more human-readable, the 4 octets of an IP are typically displayed in decimal notation, separated by dots (example: `192.168.0.2` is equivalent to the series of 4 octets `11000000.10101000.00000000.00000010`, which computers would actually store without the dots as `11000000101010000000000000000010`).

### IPv6
As there are only $2^{32}=4\,294\,967\,296$ unique IP addresses (and some IP ranges are even reserved or private, i.e. not usable for public addresses), a new standard soon became necessary. IPv6 addresses were introduced, which are 128 bits long, resulting in significantly more available addresses ($2^{128}=340\,282\,366\,920\,938\,463\,463\,374\,607\,431\,768\,211\,456$).

The human-readable notation for IPv6 addresses uses 8 groups of 16 bits in hexadecimal notation, instead of the 4 groups of 8 bits in decimal notation that IPv4 uses. So an example IPv6 address may look like `2001:0db8:85a3:0000:0000:8a2e:0370:7334`. There are also additional conventions such as using lowercase letters for the hexadecimal numbers and abbreviating runs of zeroes across _multiple_ 16-bit fields with `::` (cf. [wiki page](https://en.wikipedia.org/wiki/IPv6_address#Representation)). This way, certain addresses can be simplified significantly, e.g. the localhost (loopback) address `0:0:0:0:0:0:0:1` can be simplified to `::1`,. or the [unspecified address](https://en.wikipedia.org/wiki/IPv6_address#Unspecified_address) `0:0:0:0:0:0:0:0` just becomes `::`.

## Reserved addresses
