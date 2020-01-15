---
title: Choose a public DNS server for more privacy
date: 2020-01-15T19:56:35+01:00
---

## Choose a public DNS server for more privacy ##

You want to choose public DNS servers in KISS mode (Keep It Simple and Stupid) ?

So prepend a nameserver in resolv.conf 


* create (if not exits) /etc/dhclient.conf file with

```
interface "eth0" {
    prepend domain-name-servers 9.9.9.9;
}
```

* for testing purpose

```
dhclient eth0 -v
cat /etc/resolv.conf
```

* by this way, it will be the first DNS server to be querying for domain name.
