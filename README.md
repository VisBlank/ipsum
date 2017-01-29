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

Wall of shame (2017-01-29)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.77|11
197.231.221.211|10
89.234.157.254|9
65.19.167.132|9
176.10.104.240|9
185.56.82.66|9
163.172.209.46|9
60.11.118.110|8
128.52.128.105|8
171.25.193.131|8
203.162.37.206|8
183.129.255.34|8
192.36.27.4|8
109.163.234.7|8
191.96.249.48|8
221.194.47.224|8
216.239.90.19|8
178.217.187.39|8
121.18.238.104|8
121.18.238.109|8
218.3.140.74|8
115.239.248.35|8
151.80.42.102|8
144.12.78.162|8
123.16.86.176|8
198.57.188.180|8
37.49.224.115|8
163.172.67.180|8
115.85.192.40|8
223.255.145.158|8
77.247.181.165|8
