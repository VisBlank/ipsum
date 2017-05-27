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

**Important:** If you are planning to use `git` to get the content of this repository do it like `git clone --depth 1 https://github.com/stamparm/ipsum.git`

Wall of shame (2017-05-27)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
171.25.193.131|10
64.113.32.29|10
171.25.193.77|10
62.102.148.67|10
192.42.116.16|10
166.70.207.2|10
78.109.23.1|9
155.4.230.97|9
197.231.221.211|9
171.25.193.78|9
192.99.13.206|9
193.70.95.180|9
216.218.222.11|9
71.6.146.185|9
62.210.37.82|9
192.160.102.164|9
199.87.154.255|9
193.90.12.86|9
62.210.105.116|9
176.126.252.12|9
176.126.252.11|9
193.90.12.90|9
85.248.227.164|9
77.247.181.165|9
51.15.53.83|8
94.142.242.84|8
93.174.95.106|8
218.2.197.240|8
171.25.193.25|8
65.19.167.132|8
94.102.49.193|8
195.123.212.34|8
91.197.234.102|8
94.242.246.23|8
185.170.42.4|8
193.15.16.4|8
176.10.104.243|8
212.21.66.6|8
80.82.77.139|8
178.217.187.39|8
71.6.146.186|8
178.20.55.16|8
128.52.128.105|8
216.218.222.12|8
207.244.70.35|8
198.96.155.3|8
163.172.67.180|8
51.255.202.66|8
162.247.73.206|8
112.133.193.188|8
163.172.178.242|8
