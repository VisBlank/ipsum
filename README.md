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

Wall of shame (2017-02-16)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.77|11
89.234.157.254|10
197.231.221.211|10
37.220.35.202|9
121.18.238.109|9
195.3.144.213|9
185.110.132.202|9
200.93.235.115|8
119.249.54.71|8
113.122.13.77|8
128.52.128.105|8
171.25.193.131|8
123.31.32.5|8
65.19.167.131|8
192.36.27.4|8
176.126.252.12|8
221.194.47.208|8
221.194.44.221|8
60.12.119.222|8
221.194.47.224|8
171.25.193.78|8
176.10.104.243|8
178.217.187.39|8
71.6.146.185|8
185.129.62.63|8
173.254.216.66|8
221.194.44.219|8
125.211.216.157|8
166.70.207.2|8
93.115.95.201|8
185.38.14.171|8
91.197.235.12|8
37.187.129.166|8
77.247.181.165|8
93.103.179.52|8
181.57.149.131|8
