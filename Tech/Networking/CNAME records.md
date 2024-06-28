CNAME stands for 'canonical name'. Contrary to [A records](A%20records.md), CNAME records resolve a domain name to _another domain name_. So, after a lookup for a CNAME record, _another_ lookup for the domain that is returned will have to be initiated. This can in turn return another CNAME record. The process ends as soon after we got back an A record and consequently an IP address.