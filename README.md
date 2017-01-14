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

Wall of shame (2017-01-14)
----

|IP|Number of (black)lists|
|---|--:|
128.52.128.105|10
176.126.252.12|10
171.25.193.77|10
178.217.187.39|10
89.234.157.254|9
109.163.234.9|9
78.129.171.131|9
218.3.140.74|9
192.42.116.16|9
173.254.216.66|9
185.56.82.66|9
176.126.252.11|9
121.123.153.46|8
221.204.224.56|8
171.25.193.131|8
203.162.37.206|8
122.4.64.68|8
197.231.221.211|8
123.31.31.62|8
123.31.34.18|8
62.210.198.162|8
171.25.193.78|8
221.194.47.229|8
223.220.159.149|8
221.204.224.54|8
221.204.224.59|8
125.212.242.15|8
123.85.190.137|8
78.109.24.109|8
37.187.129.166|8
