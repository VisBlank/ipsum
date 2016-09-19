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

Wall of shame (2016-09-19)
----

|IP|Number of (black)lists|
|---|--:|
115.239.248.35|10
191.96.249.37|9
61.51.18.101|9
37.48.93.217|9
115.85.192.40|9
93.174.93.50|9
222.186.21.35|9
185.110.132.201|9
203.171.187.8|9
222.124.18.147|8
125.212.248.85|8
91.224.161.69|8
41.128.185.15|8
222.186.50.218|8
103.250.226.246|8
176.126.252.11|8
91.224.161.103|8
218.200.16.12|8
211.51.194.80|8
115.239.248.54|8
221.210.200.245|8
61.178.42.242|8
118.102.177.164|8
91.201.236.50|8
111.73.45.16|8
192.42.116.16|8
178.162.205.26|8
91.224.160.108|8
77.247.181.165|8
