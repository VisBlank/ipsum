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

Wall of shame (2017-05-14)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
185.129.62.63|11
171.25.193.131|10
176.126.252.11|10
64.113.32.29|10
171.25.193.77|10
77.109.139.87|10
111.40.166.130|10
71.6.146.185|10
128.52.128.105|10
173.254.216.66|10
51.255.202.66|10
80.82.77.139|9
92.222.84.136|9
197.231.221.211|9
65.19.167.131|9
65.19.167.132|9
87.118.126.150|9
195.154.251.209|9
176.10.104.240|9
212.21.66.6|9
178.217.187.39|9
62.102.148.67|9
71.6.146.186|9
46.166.139.71|9
192.160.102.164|9
192.42.116.16|9
85.248.227.163|9
176.126.252.12|9
77.247.181.165|9
77.247.181.163|9
51.15.53.83|8
198.20.69.98|8
185.188.205.2|8
198.245.60.8|8
171.25.193.132|8
185.165.168.92|8
192.36.27.4|8
94.102.49.190|8
193.90.12.90|8
91.213.8.236|8
37.218.245.25|8
193.70.95.180|8
192.160.102.166|8
166.70.207.2|8
163.172.67.180|8
37.187.129.166|8
85.248.227.164|8
