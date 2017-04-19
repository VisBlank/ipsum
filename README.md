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

Wall of shame (2017-04-19)
----

|IP|Number of (black)lists|
|---|--:|
176.126.252.11|12
173.254.216.66|12
94.142.242.84|11
171.25.193.77|11
128.52.128.105|10
94.242.246.24|10
209.222.77.220|10
64.113.32.29|10
62.102.148.67|10
37.123.133.148|10
89.234.157.254|10
61.158.207.152|9
61.183.117.250|9
171.25.193.131|9
197.231.221.211|9
192.36.27.4|9
109.163.234.5|9
111.40.166.130|9
176.10.104.243|9
91.197.232.108|9
176.126.252.12|9
192.160.102.166|9
166.70.207.2|9
77.247.181.165|9
185.170.41.8|8
114.255.78.181|8
93.174.95.106|8
91.197.232.109|8
91.197.232.107|8
171.25.193.132|8
207.244.70.35|8
80.82.77.139|8
163.172.136.101|8
171.25.193.25|8
220.171.31.163|8
50.235.31.42|8
109.163.234.2|8
60.2.127.118|8
114.255.78.180|8
122.97.218.114|8
171.25.193.78|8
91.236.116.77|8
212.21.66.6|8
71.6.146.186|8
71.6.146.185|8
171.13.138.226|8
195.3.144.216|8
27.148.248.21|8
185.129.62.63|8
185.129.62.62|8
89.248.168.30|8
218.60.136.106|8
199.87.154.255|8
163.172.67.180|8
119.147.144.140|8
192.42.116.16|8
193.90.12.87|8
81.100.183.189|8
62.210.105.116|8
119.249.54.93|8
85.248.227.163|8
77.247.181.163|8
