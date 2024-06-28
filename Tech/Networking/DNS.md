The Domain Name System is essentially the phonebook of the internet (according to [CloudFlare](https://www.cloudflare.com/learning/dns/what-is-dns/)). Under the hood, every web browser accesses IP adresses, but of course users prefer accessing websites via easy-to-remember domain names (e.g. example.com). DNS accomplishes this task of mapping domain names to IP adresses.

## How DNS lookup works
There are four types of servers involved in a DNS lookup
1. Recursive resolvers
2. root nameservers
3. TLD nameservers
4. authoritative nameserver

In practice, caching can be involved. But initially, lookup works somehow like this:
![Source: https://www.cloudflare.com/img/learning/dns/dns-server-types/recursive-resolver.png](Pasted%20image%2020240612132409.png)
