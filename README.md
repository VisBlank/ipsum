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

Wall of shame (2017-04-14)
----

|IP|Number of (black)lists|
|---|--:|
173.254.216.66|11
128.52.128.105|10
197.231.221.211|10
209.222.77.220|10
109.163.234.5|10
64.113.32.29|10
166.70.207.2|10
89.234.157.254|10
94.142.242.84|9
94.242.246.24|9
80.82.70.134|9
60.255.146.181|9
114.255.78.180|9
171.25.193.77|9
171.25.193.78|9
111.40.166.130|9
176.10.104.243|9
62.102.148.67|9
71.6.146.185|9
91.197.232.108|9
176.126.252.11|9
185.165.29.44|9
222.85.219.9|9
193.90.12.89|9
176.126.252.12|9
49.4.135.20|9
61.183.117.250|8
91.197.232.11|8
91.197.232.109|8
91.197.232.107|8
171.25.193.131|8
207.244.70.35|8
60.165.208.28|8
163.172.136.101|8
94.242.246.23|8
65.19.167.131|8
192.36.27.4|8
94.102.49.190|8
91.223.82.156|8
222.161.200.123|8
109.163.234.2|8
71.6.146.186|8
60.2.127.118|8
77.109.139.87|8
130.226.169.137|8
113.209.68.135|8
193.201.224.215|8
122.194.212.177|8
176.10.104.240|8
212.21.66.6|8
122.116.214.130|8
195.3.144.215|8
113.122.1.107|8
89.248.167.131|8
77.247.181.163|8
221.122.101.203|8
185.129.62.63|8
46.166.148.177|8
192.160.102.166|8
221.210.200.245|8
116.252.34.161|8
37.123.133.148|8
195.3.144.216|8
192.42.116.16|8
119.249.54.93|8
77.247.181.165|8
