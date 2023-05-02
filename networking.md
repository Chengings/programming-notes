# Networking

📦
 - [MTR](https://en.wikipedia.org/wiki/MTR_(software))
 - [BGP: HE](https://bgp.he.net/)
 - [BGP: bgp.tools](https://bgp.tools)
 - [Peering DB](https://www.peeringdb.com/)
 - [Speedtest: Cloudflare](https://speed.cloudflare.com/)
 - [Speedtest: Netflix](https://fast.com/)
 - [Speedtest + Ping: testmy.net](https://testmy.net)
 - [Dns leak test](https://dnsleaktest.com/)
 - [Dns performance](https://www.dnsperf.com/)
 - [am.i.mullvad.net](https://mullvad.net/en/check/)
 - [Ipleak](https://ipleak.net/)
 - [IP Address Fraud Checker: Scamalytics](https://scamalytics.com/)
 - [IP Address Geolocation: BigDataCloud](https://www.bigdatacloud.com/ip-geolocation/what-is-my-ip)
 - [IP Address Geolocation: ipdata](https://ipdata.co/)

📚
 * [Diagnosing Network Issues with MTR](https://www.linode.com/docs/networking/diagnostics/diagnosing-network-issues-with-mtr/)
 * https://en.wikipedia.org/wiki/IEEE_802
 * [The pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/preface/index.html)
 * [Cloudflare: Measuring network quality to better understand the end-user experience](https://blog.cloudflare.com/aim-database-for-internet-quality/)
---

## Domain Name System (https://en.wikipedia.org/wiki/Domain_Name_System)

[Reserved Domains](https://en.wikipedia.org/wiki/Top-level_domain#Reserved_domains)

[Addressing the challenges of modern DNS a comprehensive tutorial](https://www.sciencedirect.com/science/article/pii/S1574013722000132)

## NTP and About Time

> NTP  uses  __UTC__,  as  distinct  from  the  Greenwich  Mean  Time  (GMT),  as  the  reference  clock  standard.  UTC  uses  the  TAI  time  standard.
>
> NTP is an “absolute” time protocol. This conversion from UTC to the wall-clock time, namely the local date and time, is left to the local host.
>
> NTP operates over the User Datagram Protocol (UDP). An NTP server listens for client NTP packets on port 123.
>
> Clustering of the time signals is performed to reject outlier servers, and then the algorithm __selects the server with the lowest stratum with minimal offset and jitter values__. The algorithm used by NTP to perform this operation is Marzullo’s Algorithm
>
> When NTP is configured on a client, it attempts to keep the client clock synchronized against the reference time standard. To do this task NTP conventionally __adjusts the local time by small offsets__ (larger offsets may cause side effects on running applications, as has been found when processing leap seconds). This small adjustment is undertaken by an adjtime() system call, which slews the clock by altering the frequency of the software clock until the time correction is achieved
>
> The ISP Column  A monthly column on things Internet,  March 2014 , Geoff Huston

### My gist

* Use chrony if possible. Red Hat, Fedora, Amazon and Facebook switched to this software.
* Use 4+ various time sources, e.g. tech giant, academic/non-profit, official  and NTP pool.

### Use Enough Time Sources

Sources SHOULD be diverse. Having more than 4 sources are reliability.

References:
* https://datatracker.ietf.org/doc/html/rfc8633#section-3.2
* https://docs.ntpsec.org/latest/quick.html#howmany

### Use cases of NTP

* Authentication + Encryption: TOTP, LDAP, RADIUS, SSL + TLS, IPSEC, DNSSEC
* Logging
* Scheduled tasks/events: cron

References:
* https://digital.nhs.uk/services/health-and-social-care-network/hscn-technical-guidance/hscn-network-time-protocol-guidance

### Public NTP services

🧙🏻‍♂️: Official timekeeper
🔐: DNSSEC
🛰: GNSS
⚛️: Atomic clock
🗼: Radio time singal

[SIDN Labs 🔐🛰🗼🇳🇱](https://time.nl/index_en.html)

[National Physical Laboratory 🧙🏻‍♂️⚛️🇬🇧](https://www.npl.co.uk/products-services/time-frequency/internet-time)

[Swedish Distributed Time Service 🧙🏻‍♂️🔐⚛️🇸🇪](https://www.ntp.se/)

[Google Public NTP ⚛️](https://developers.google.com/time/)

[Facebook Public NTP 🛰⚛️](https://engineering.fb.com/2020/03/18/production-engineering/ntp-service/)

[Cloudflare Time Services 🔐](https://www.cloudflare.com/en-gb/time/)

[Physikalisch-Technische Bundesanstalt 🧙🏻‍♂️🔐⚛️🇩🇪](https://www.ptb.de/cms/en/ptb/fachabteilungen/abtq/gruppe-q4/ref-q42/time-synchronization-of-computers-using-the-network-time-protocol-ntp.html)

### See Also

https://chrony.tuxfamily.org/

https://weberblog.net/ntp/

https://www.satsignal.eu/ntp/index.html

Reference Clock Support https://docs.ntpsec.org/latest/refclock.html and also check their site for manual and configurations (detailed).

## Wireguard (https://www.wireguard.com/)

⭐️ [Some Unofficial WireGuard Documentation](https://github.com/pirate/wireguard-docs)

[WireGuard support and deployment: ianix](https://ianix.com/wireguard/wireguard-deployment.html)

[Wireguard: archlinux](https://wiki.archlinux.org/index.php/WireGuard)

## Link-local address

Link-local addresses are used for communication between two hosts (which are there on the same link) when no other IP address is specified.

In simple words, at the time of booting up, OS tries to configure an address on its interface through various methods like

-   Manual Configuration
-   DHCP (DHCPv4 or DHCPv6)
-   SLAAC (Stateless Autoconfiguration) -- Unique to IPv6

And if ==OS isn't able to configure an address on the interface through any of the automatic methods, then it configures an address on the interface from the link-local pool.==

-   169.254.0.0/16 -- Link-local address pool in IPv4 address space
-   fe80::/10 -- Link-local address pool in IPv6 address space

### See also
* https://en.wikipedia.org/wiki/Link-local_address
* https://networkengineering.stackexchange.com/a/35959

