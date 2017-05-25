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

Wall of shame (2017-05-25)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.131|12
89.234.157.254|12
166.70.207.2|11
64.113.32.29|11
171.25.193.77|11
192.99.13.206|11
62.102.148.67|11
192.42.116.16|11
78.109.23.1|10
51.255.202.66|10
193.70.95.180|10
216.218.222.11|10
176.126.252.12|10
163.172.67.180|10
62.210.105.116|10
85.248.227.164|10
77.247.181.165|10
94.23.173.249|9
51.15.53.83|9
218.2.197.240|9
207.244.70.35|9
155.4.230.97|9
77.109.139.87|9
171.25.193.78|9
193.15.16.4|9
176.10.104.243|9
212.21.66.6|9
80.82.77.139|9
128.52.128.105|9
192.160.102.164|9
173.254.216.66|9
85.248.227.165|9
198.96.155.3|9
199.87.154.255|9
193.90.12.86|9
193.90.12.89|9
176.126.252.11|9
193.90.12.90|9
94.142.242.84|8
93.174.95.106|8
185.117.215.9|8
164.132.51.91|8
93.115.95.204|8
93.115.95.205|8
163.172.136.101|8
197.231.221.211|8
65.19.167.130|8
65.19.167.132|8
65.19.167.134|8
109.163.234.9|8
109.163.234.4|8
109.163.234.5|8
109.163.234.7|8
109.163.234.2|8
171.25.193.20|8
195.123.212.34|8
80.67.172.162|8
185.100.84.82|8
130.226.169.137|8
91.197.234.102|8
94.242.246.23|8
185.170.42.4|8
111.40.166.130|8
87.118.126.150|8
128.127.105.159|8
198.20.70.114|8
178.217.187.39|8
71.6.146.186|8
71.6.146.185|8
89.248.172.16|8
62.210.37.82|8
51.15.40.233|8
185.129.62.63|8
46.165.230.5|8
92.222.69.25|8
216.218.222.12|8
185.38.14.171|8
37.220.35.202|8
37.187.129.166|8
60.191.38.78|8
58.20.95.117|8
85.248.227.163|8
