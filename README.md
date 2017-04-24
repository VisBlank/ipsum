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

Wall of shame (2017-04-24)
----

|IP|Number of (black)lists|
|---|--:|
94.142.242.84|11
89.234.157.254|11
171.25.193.77|11
197.231.221.211|10
109.163.234.5|10
64.113.32.29|10
193.15.16.4|10
62.102.148.67|10
128.52.128.105|10
61.158.207.152|9
171.25.193.131|9
171.25.193.132|9
209.222.77.220|9
114.255.78.181|9
111.40.166.130|9
176.10.104.243|9
71.6.146.185|9
176.126.252.12|9
89.248.168.30|9
173.254.216.66|9
216.218.222.12|9
77.247.181.163|9
37.123.133.148|9
176.126.252.11|9
77.247.181.165|9
94.242.246.24|9
222.187.86.51|8
80.82.77.33|8
173.79.162.220|8
165.231.0.242|8
91.197.232.109|8
91.197.232.107|8
207.244.70.35|8
80.82.77.139|8
119.78.254.4|8
65.19.167.131|8
50.235.31.42|8
183.129.255.34|8
109.163.234.8|8
80.82.66.60|8
60.2.127.118|8
114.255.78.180|8
193.201.224.210|8
122.97.218.114|8
171.25.193.78|8
115.238.248.9|8
176.10.104.240|8
82.221.105.6|8
71.6.146.186|8
119.160.197.102|8
195.3.144.213|8
91.197.232.108|8
68.195.9.243|8
51.15.40.233|8
221.122.101.203|8
163.172.197.79|8
163.172.73.217|8
199.87.154.255|8
222.85.219.9|8
108.59.9.89|8
163.172.67.180|8
112.91.82.252|8
192.42.116.16|8
193.90.12.89|8
195.154.217.29|8
