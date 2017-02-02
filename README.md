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

Wall of shame (2017-02-02)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|10
178.217.187.39|10
118.175.31.131|9
197.231.221.211|9
209.222.77.220|9
123.31.34.18|9
176.10.104.240|9
212.21.66.6|9
185.129.62.62|9
173.254.216.66|9
111.200.254.137|9
192.42.116.16|9
124.160.59.196|8
211.71.30.103|8
128.52.128.105|8
171.25.193.131|8
176.126.252.12|8
109.163.234.7|8
37.220.35.202|8
221.194.44.221|8
171.25.193.77|8
39.66.98.210|8
46.166.148.142|8
216.239.90.19|8
115.239.248.35|8
178.20.55.16|8
151.80.42.102|8
51.15.40.233|8
93.103.179.52|8
37.49.224.115|8
46.166.148.176|8
163.172.67.180|8
85.93.218.204|8
185.38.14.171|8
51.255.202.66|8
203.110.165.2|8
185.110.132.202|8
163.172.209.46|8
