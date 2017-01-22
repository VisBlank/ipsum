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

Wall of shame (2017-01-22)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|10
65.19.167.132|10
171.25.193.77|10
166.70.207.2|10
128.52.128.105|9
197.231.221.211|9
109.163.234.9|9
176.10.104.243|9
176.10.104.240|9
46.148.17.18|9
173.254.216.66|9
192.42.116.16|9
185.38.14.171|9
77.247.181.165|9
62.210.81.52|8
203.162.37.206|8
217.115.10.131|8
222.255.174.50|8
192.36.27.6|8
209.222.77.220|8
176.126.252.12|8
109.163.234.7|8
123.31.34.18|8
191.96.249.8|8
191.96.249.48|8
37.220.35.202|8
95.211.205.151|8
81.212.109.229|8
171.25.193.78|8
199.87.154.255|8
178.217.187.39|8
151.80.42.102|8
149.56.229.16|8
115.239.230.227|8
93.103.179.52|8
193.90.12.87|8
193.90.12.89|8
185.56.82.66|8
85.93.218.204|8
163.172.209.46|8
163.172.170.212|8
101.200.60.75|8
