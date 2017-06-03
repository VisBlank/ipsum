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

Wall of shame (2017-06-03)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.131|11
89.234.157.254|11
64.113.32.29|11
166.70.207.2|11
171.25.193.77|10
218.2.197.240|9
207.244.70.35|9
78.109.23.1|9
155.4.230.97|9
197.231.221.211|9
176.126.252.12|9
171.25.193.78|9
193.70.95.180|9
62.102.148.67|9
192.42.116.16|9
62.210.105.116|9
176.126.252.11|9
51.255.202.66|9
193.90.12.90|9
85.248.227.164|9
77.247.181.165|9
51.15.53.83|8
94.142.242.84|8
94.242.246.24|8
93.174.95.47|8
130.226.169.137|8
146.185.177.103|8
62.210.37.82|8
111.40.166.130|8
193.15.16.4|8
212.21.66.6|8
80.82.77.139|8
178.217.187.39|8
71.6.146.186|8
46.165.230.5|8
115.182.100.37|8
192.160.102.164|8
173.254.216.66|8
85.248.227.165|8
91.197.234.102|8
199.87.154.255|8
163.172.67.180|8
193.90.12.87|8
79.124.59.202|8
60.191.38.78|8
216.218.222.11|8
112.133.193.188|8
