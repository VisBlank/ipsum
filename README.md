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

Wall of shame (2017-04-16)
----

|IP|Number of (black)lists|
|---|--:|
62.102.148.67|12
176.126.252.11|12
128.52.128.105|11
89.234.157.254|11
109.163.234.5|11
173.254.216.66|11
94.142.242.84|10
171.25.193.131|10
94.242.246.24|10
197.231.221.211|10
192.36.27.4|10
209.222.77.220|10
64.113.32.29|10
171.25.193.77|10
176.10.104.243|10
166.70.207.2|10
94.242.246.23|9
91.197.232.108|9
46.166.148.177|9
192.42.116.16|9
176.126.252.12|9
77.247.181.163|9
222.187.86.51|8
93.174.95.106|8
91.197.232.109|8
91.197.232.107|8
207.244.70.35|8
80.82.77.139|8
93.115.95.202|8
171.25.193.25|8
80.82.70.134|8
50.235.31.42|8
183.129.255.34|8
60.255.146.181|8
192.36.27.7|8
222.161.200.123|8
109.163.234.2|8
5.196.1.129|8
60.2.127.118|8
77.109.139.87|8
114.255.78.180|8
114.255.78.181|8
122.194.44.206|8
171.25.193.78|8
222.184.79.60|8
111.40.166.130|8
122.194.212.177|8
71.6.146.186|8
121.30.232.162|8
176.10.104.240|8
212.21.66.6|8
71.6.146.185|8
51.15.40.233|8
221.122.101.203|8
185.129.62.63|8
46.165.230.5|8
122.192.59.107|8
122.224.40.84|8
192.160.102.166|8
221.210.200.245|8
199.87.154.255|8
85.248.227.165|8
193.90.12.87|8
193.90.12.86|8
113.122.47.186|8
49.4.135.20|8
85.248.227.163|8
77.247.181.165|8
119.193.140.213|8
