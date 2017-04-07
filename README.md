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

Wall of shame (2017-04-07)
----

|IP|Number of (black)lists|
|---|--:|
128.52.128.105|10
89.234.157.254|10
197.231.221.211|10
209.222.77.220|10
89.248.168.30|10
166.70.207.2|10
181.57.149.131|10
176.10.104.243|9
94.242.246.24|9
171.25.193.77|9
111.40.166.130|9
178.217.187.39|9
176.126.252.12|9
111.40.168.90|9
37.187.129.166|9
94.142.242.84|8
223.197.203.122|8
91.197.232.108|8
117.79.156.130|8
114.255.78.181|8
130.226.169.137|8
212.47.242.127|8
193.15.16.4|8
212.21.66.6|8
80.82.77.139|8
62.102.148.67|8
71.6.146.186|8
71.6.146.185|8
190.7.129.126|8
221.122.101.203|8
122.192.59.107|8
173.254.216.66|8
112.120.150.123|8
77.247.181.163|8
37.123.133.148|8
192.42.116.16|8
176.126.252.11|8
113.122.7.255|8
