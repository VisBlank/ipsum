![Logo](logo.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2017-02-05)
----

|IP|Number of (black)lists|
|---|--:|
178.217.187.39|11
89.234.157.254|10
197.231.221.211|10
171.25.193.77|10
209.222.77.220|9
173.254.216.66|9
223.255.145.158|9
176.10.104.240|8
61.172.252.70|8
128.52.128.105|8
171.25.193.131|8
221.215.160.138|8
185.38.14.171|8
123.31.34.18|8
61.159.190.254|8
191.96.249.48|8
37.220.35.202|8
117.71.18.20|8
46.166.148.176|8
202.55.21.43|8
176.10.104.243|8
212.21.66.6|8
60.205.190.89|8
151.80.42.102|8
51.15.46.217|8
221.194.44.219|8
111.198.24.196|8
118.192.177.68|8
163.172.67.180|8
185.110.132.202|8
80.90.196.148|8
163.172.112.59|8
