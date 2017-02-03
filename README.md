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

Wall of shame (2017-02-03)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|10
197.231.221.211|10
178.217.187.39|10
118.175.31.131|9
109.163.234.7|9
123.31.34.18|9
171.25.193.77|9
51.15.40.233|9
173.254.216.66|9
223.255.145.158|9
176.10.104.240|8
124.160.59.196|8
128.52.128.105|8
171.25.193.131|8
93.115.95.202|8
222.141.64.65|8
209.222.77.220|8
176.126.252.12|8
191.96.249.48|8
37.220.35.202|8
5.196.1.129|8
46.166.148.176|8
39.66.98.210|8
212.21.66.6|8
185.40.4.23|8
193.201.224.39|8
115.239.248.35|8
151.80.42.102|8
185.129.62.62|8
111.200.254.137|8
192.42.116.16|8
193.90.12.89|8
185.38.14.171|8
51.255.202.66|8
203.110.165.2|8
185.110.132.202|8
85.248.227.164|8
163.172.170.212|8
