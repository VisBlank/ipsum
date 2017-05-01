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

Wall of shame (2017-05-01)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
171.25.193.77|11
62.102.148.67|11
128.52.128.105|10
171.25.193.131|10
109.163.234.7|10
185.170.42.4|10
199.87.154.255|10
94.142.242.84|9
165.231.0.242|9
198.20.69.98|9
80.82.77.139|9
87.118.126.150|9
209.222.77.220|9
109.163.234.8|9
109.163.234.5|9
111.40.166.130|9
193.15.16.4|9
112.17.8.241|9
212.21.66.6|9
71.6.146.185|9
89.248.168.30|9
192.160.102.164|9
173.254.216.66|9
192.42.116.16|9
163.172.67.180|9
77.247.181.163|9
185.170.41.8|8
94.23.173.249|8
61.177.21.226|8
185.117.215.9|8
164.132.51.91|8
92.222.84.136|8
197.231.221.211|8
82.221.105.6|8
94.102.49.190|8
94.102.49.193|8
109.163.234.9|8
130.226.169.137|8
64.113.32.29|8
216.218.222.12|8
122.97.218.114|8
171.25.193.78|8
176.10.104.243|8
176.10.104.240|8
71.6.146.186|8
71.6.158.166|8
91.197.232.108|8
51.15.40.233|8
109.163.234.2|8
51.255.202.66|8
213.61.149.100|8
137.74.167.96|8
195.154.217.29|8
188.138.57.209|8
