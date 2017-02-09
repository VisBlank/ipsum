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

Wall of shame (2017-02-09)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|10
110.167.224.182|9
185.38.14.171|9
37.220.35.202|9
171.25.193.77|9
218.2.108.2|9
176.10.104.243|9
221.204.224.54|9
178.217.187.39|9
181.57.149.131|9
119.249.54.71|8
94.142.242.84|8
191.96.249.33|8
185.38.14.215|8
123.31.34.126|8
207.244.70.35|8
197.231.221.211|8
65.19.167.131|8
192.36.27.4|8
209.222.77.220|8
176.126.252.12|8
109.163.234.7|8
123.31.34.18|8
191.96.249.48|8
210.212.182.184|8
64.113.32.29|8
123.31.41.149|8
193.201.224.210|8
171.25.193.78|8
27.208.47.55|8
95.128.43.164|8
113.122.44.252|8
157.25.102.210|8
185.159.36.10|8
151.80.42.102|8
91.73.174.66|8
51.255.33.0|8
149.56.229.16|8
192.160.102.166|8
192.160.102.164|8
109.163.234.4|8
191.96.249.110|8
176.123.27.28|8
111.198.24.196|8
166.70.207.2|8
173.254.216.66|8
163.172.67.180|8
192.42.116.16|8
51.255.202.66|8
91.197.235.12|8
37.187.129.166|8
185.110.132.202|8
85.248.227.163|8
77.247.181.165|8
