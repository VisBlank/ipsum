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

Wall of shame (2017-05-13)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
128.52.128.105|11
171.25.193.131|10
64.113.32.29|10
171.25.193.77|10
77.109.139.87|10
173.254.216.66|10
166.70.207.2|10
51.255.202.66|10
80.82.77.139|9
92.222.84.136|9
65.19.167.131|9
65.19.167.132|9
87.118.126.150|9
111.40.166.130|9
216.218.222.11|9
176.10.104.240|9
212.21.66.6|9
178.217.187.39|9
62.102.148.67|9
71.6.146.186|9
71.6.146.185|9
185.129.62.63|9
46.166.139.71|9
192.160.102.166|9
192.160.102.164|9
176.126.252.11|9
77.247.181.165|9
77.247.181.163|9
94.242.246.24|9
185.170.41.8|8
93.174.95.106|8
198.245.60.8|8
217.182.71.208|8
164.132.51.91|8
163.172.136.101|8
204.8.156.142|8
218.78.213.142|8
197.231.221.211|8
65.19.167.130|8
192.36.27.4|8
195.154.251.209|8
185.170.42.4|8
193.70.95.180|8
176.10.104.243|8
192.42.116.16|8
163.172.67.180|8
193.90.12.86|8
185.34.33.2|8
37.187.129.166|8
85.248.227.164|8
85.248.227.163|8
176.126.252.12|8
