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

Wall of shame (2017-04-23)
----

|IP|Number of (black)lists|
|---|--:|
64.113.32.29|12
173.254.216.66|12
89.234.157.254|12
176.126.252.11|12
128.52.128.105|11
94.242.246.24|11
94.142.242.84|10
171.25.193.131|10
209.222.77.220|10
109.163.234.5|10
62.102.148.67|10
176.126.252.12|10
37.123.133.148|10
77.247.181.165|10
185.170.41.8|9
185.117.215.9|9
197.231.221.211|9
183.129.255.34|9
114.255.78.181|9
171.25.193.77|9
111.40.166.130|9
193.15.16.4|9
176.10.104.243|9
176.10.104.240|9
51.15.40.233|9
89.248.168.30|9
199.87.154.255|9
163.172.67.180|9
193.90.12.89|9
61.158.207.152|8
158.69.215.106|8
51.15.53.83|8
61.183.117.250|8
91.197.232.109|8
91.197.232.107|8
112.91.82.252|8
65.19.167.130|8
65.19.167.131|8
65.19.167.134|8
50.235.31.42|8
192.36.27.4|8
109.163.234.8|8
77.247.159.193|8
5.196.1.129|8
114.255.78.180|8
94.242.246.23|8
171.25.193.78|8
115.238.248.9|8
222.161.200.123|8
71.6.146.185|8
91.197.232.108|8
94.102.49.193|8
221.122.101.203|8
192.160.102.166|8
91.213.8.84|8
216.218.222.12|8
218.60.136.106|8
192.42.116.16|8
166.70.207.2|8
188.92.75.10|8
91.236.116.77|8
119.249.54.93|8
85.248.227.163|8
221.194.44.190|8
