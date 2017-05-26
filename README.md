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

Wall of shame (2017-05-26)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.131|11
89.234.157.254|11
166.70.207.2|11
171.25.193.77|10
192.42.116.16|10
193.90.12.86|10
176.126.252.12|10
85.248.227.164|10
78.109.23.1|9
197.231.221.211|9
64.113.32.29|9
171.25.193.78|9
192.99.13.206|9
193.70.95.180|9
62.102.148.67|9
71.6.146.186|9
62.210.37.82|9
199.87.154.255|9
163.172.67.180|9
62.210.105.116|9
176.126.252.11|9
51.255.202.66|9
193.90.12.90|9
77.247.181.165|9
51.15.53.83|8
93.174.95.106|8
218.2.197.240|8
155.4.230.97|8
65.19.167.132|8
94.102.49.190|8
94.102.49.193|8
171.25.193.20|8
77.109.139.87|8
91.197.234.102|8
185.170.42.4|8
111.40.166.130|8
216.218.222.11|8
176.10.104.243|8
212.21.66.6|8
198.20.70.114|8
80.82.77.139|8
178.217.187.39|8
71.6.146.185|8
89.248.172.16|8
178.20.55.16|8
128.52.128.105|8
185.129.62.62|8
192.160.102.164|8
173.254.216.66|8
207.244.70.35|8
198.96.155.3|8
163.172.178.242|8
112.133.193.188|8
