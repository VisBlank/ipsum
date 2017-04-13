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

Wall of shame (2017-04-13)
----

|IP|Number of (black)lists|
|---|--:|
166.70.207.2|12
94.142.242.84|11
128.52.128.105|10
94.242.246.24|10
197.231.221.211|10
209.222.77.220|10
176.126.252.11|10
109.163.234.5|10
171.25.193.77|10
89.248.168.30|10
173.254.216.66|10
89.234.157.254|10
61.183.117.250|9
114.255.78.180|9
114.255.78.181|9
171.25.193.78|9
111.40.166.130|9
122.194.212.177|9
176.10.104.243|9
62.102.148.67|9
91.197.232.108|9
176.126.252.12|9
193.90.12.86|8
91.197.232.109|8
91.197.232.107|8
171.25.193.131|8
171.25.193.132|8
80.82.77.139|8
171.25.193.25|8
65.19.167.131|8
183.129.255.34|8
218.5.241.13|8
60.255.146.181|8
192.36.27.7|8
109.163.234.2|8
71.6.146.186|8
130.226.169.137|8
94.242.246.23|8
113.209.68.135|8
92.222.69.25|8
222.184.79.60|8
176.10.104.240|8
212.21.66.6|8
82.221.105.6|8
222.161.200.123|8
71.6.146.185|8
195.3.144.213|8
111.40.168.90|8
89.144.12.15|8
77.247.181.163|8
221.122.101.203|8
51.15.40.233|8
115.182.100.37|8
192.160.102.166|8
207.244.70.35|8
27.208.114.208|8
144.0.239.71|8
37.123.133.148|8
192.42.116.16|8
193.90.12.87|8
85.248.227.163|8
77.247.181.165|8
