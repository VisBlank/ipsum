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

Wall of shame (2017-01-13)
----

|IP|Number of (black)lists|
|---|--:|
128.52.128.105|9
89.234.157.254|9
197.231.221.211|9
123.31.34.18|9
64.113.32.29|9
171.25.193.77|9
178.217.187.39|9
176.126.252.11|9
221.194.44.229|9
37.187.129.166|9
221.204.224.56|8
122.4.64.68|8
65.19.167.131|8
51.15.57.90|8
123.31.31.62|8
209.222.77.220|8
176.126.252.12|8
109.163.234.9|8
191.96.249.48|8
62.210.198.162|8
94.242.246.24|8
221.194.47.229|8
171.25.193.78|8
31.184.195.114|8
218.3.140.74|8
125.212.242.15|8
151.80.42.102|8
106.166.151.40|8
123.85.190.137|8
78.109.24.109|8
192.42.116.16|8
166.70.207.2|8
173.254.216.66|8
185.56.82.66|8
61.142.176.23|8
93.49.172.140|8
