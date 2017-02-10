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

Wall of shame (2017-02-10)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
207.244.70.35|10
178.217.187.39|10
110.167.224.182|9
165.231.0.242|9
128.52.128.105|9
171.25.193.131|9
197.231.221.211|9
192.36.27.4|9
176.126.252.12|9
94.242.246.24|9
171.25.193.77|9
176.10.104.243|9
192.160.102.164|9
191.96.249.110|9
166.70.207.2|9
173.254.216.66|9
185.38.14.171|9
176.126.252.11|9
37.187.129.166|9
185.110.132.202|9
149.202.98.161|8
119.249.54.71|8
191.96.249.33|8
191.96.249.38|8
93.115.95.202|8
183.129.255.34|8
221.229.173.164|8
209.222.77.221|8
109.163.234.7|8
123.31.34.18|8
191.96.249.48|8
37.220.35.202|8
64.113.32.29|8
193.201.224.210|8
173.208.213.114|8
218.2.108.2|8
199.87.154.255|8
171.25.193.78|8
62.102.148.67|8
218.3.140.74|8
193.201.224.39|8
185.159.36.10|8
151.80.42.102|8
121.18.238.114|8
149.56.229.16|8
185.129.62.63|8
109.163.234.4|8
185.106.22.73|8
176.123.27.28|8
82.163.125.70|8
118.192.177.68|8
121.18.238.98|8
163.172.67.180|8
72.52.75.27|8
14.39.210.153|8
77.247.181.165|8
181.57.149.131|8
