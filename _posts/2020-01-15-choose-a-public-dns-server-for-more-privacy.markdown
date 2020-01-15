---
title: Choose a public DNS server for more privacy
date: 2020-01-15T19:56:35+01:00
---

You have to prepend a nameserver in resolv.conf file.

Follow this quick guide in KISS mode (Keep It Simple and Stupid).


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

* some public DNS servers easy to remember:
** 1.1.1.1  (Cloudflare)
** 9.9.9.9  (Quad9)

* [More public DNS servers](https://en.wikipedia.org/wiki/Public_recursive_name_server)
