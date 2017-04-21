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

Wall of shame (2017-04-21)
----

|IP|Number of (black)lists|
|---|--:|
94.142.242.84|11
89.234.157.254|11
94.242.246.24|11
176.126.252.11|11
173.254.216.66|11
128.52.128.105|10
171.25.193.131|10
62.102.148.67|10
37.123.133.148|10
209.222.77.220|9
109.163.234.5|9
64.113.32.29|9
171.25.193.77|9
111.40.166.130|9
91.197.232.108|9
176.126.252.12|9
51.15.40.233|9
89.248.168.30|9
166.70.207.2|9
77.247.181.165|9
61.158.207.152|8
158.69.215.106|8
93.174.95.106|8
61.183.117.250|8
91.197.232.109|8
5.8.10.202|8
197.231.221.211|8
119.78.254.4|8
50.235.31.42|8
183.129.255.34|8
112.250.104.128|8
109.163.234.2|8
210.51.191.26|8
111.202.93.14|8
60.2.127.118|8
114.255.78.180|8
114.255.78.181|8
94.242.246.23|8
113.209.68.135|8
171.25.193.78|8
49.4.135.211|8
176.10.104.243|8
91.197.232.107|8
111.40.168.90|8
192.160.102.166|8
221.210.200.245|8
199.87.154.255|8
192.42.116.16|8
85.248.227.165|8
193.90.12.86|8
193.90.12.89|8
216.218.222.12|8
