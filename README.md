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

Wall of shame (2017-04-15)
----

|IP|Number of (black)lists|
|---|--:|
166.70.207.2|12
94.142.242.84|11
128.52.128.105|11
209.222.77.220|11
109.163.234.5|11
176.126.252.11|11
173.254.216.66|11
89.234.157.254|11
197.231.221.211|10
171.25.193.77|10
62.102.148.67|10
171.25.193.131|9
94.242.246.24|9
80.82.70.134|9
192.36.27.4|9
71.6.146.185|9
176.10.104.243|9
46.166.148.177|9
192.160.102.166|9
116.252.34.161|9
192.42.116.16|9
193.90.12.86|9
176.126.252.12|9
77.247.181.165|9
77.247.181.163|9
222.187.86.51|8
91.197.232.109|8
91.197.232.107|8
171.25.193.132|8
80.82.77.139|8
60.165.208.28|8
65.19.167.132|8
60.255.146.181|8
192.36.27.7|8
94.102.49.190|8
109.163.234.2|8
77.109.139.87|8
114.255.78.180|8
114.255.78.181|8
122.194.44.206|8
64.113.32.29|8
94.242.246.23|8
171.25.193.78|8
49.4.135.211|8
111.40.166.130|8
193.15.16.4|8
122.194.212.177|8
71.6.146.186|8
121.30.232.162|8
212.21.66.6|8
195.3.144.213|8
91.197.232.108|8
89.248.167.131|8
185.129.62.63|8
51.15.40.233|8
122.224.40.84|8
185.165.29.44|8
221.210.200.245|8
122.97.218.114|8
222.85.219.9|8
37.123.133.148|8
85.248.227.165|8
195.3.144.216|8
112.91.82.252|8
193.90.12.89|8
49.4.135.20|8
119.249.54.93|8
85.248.227.163|8
193.105.134.184|8
182.44.219.144|8
