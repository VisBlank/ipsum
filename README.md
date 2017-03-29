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

Wall of shame (2017-03-29)
----

|IP|Number of (black)lists|
|---|--:|
111.40.166.130|11
178.217.187.39|10
211.234.100.203|9
221.122.101.203|9
59.44.175.164|9
181.57.149.131|9
91.197.232.108|8
128.52.128.105|8
58.246.141.205|8
89.234.157.254|8
94.242.246.24|8
176.126.252.12|8
37.220.35.202|8
114.255.78.181|8
222.47.26.18|8
221.183.16.231|8
14.23.160.11|8
211.220.207.201|8
171.25.193.77|8
111.73.46.90|8
206.221.189.34|8
163.172.73.217|8
193.15.16.4|8
27.208.114.208|8
118.180.18.102|8
111.40.30.206|8
91.236.116.77|8
37.187.129.166|8
221.194.47.198|8
