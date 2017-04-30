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

Wall of shame (2017-04-30)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|12
171.25.193.77|12
109.163.234.5|11
193.15.16.4|11
173.254.216.66|11
94.142.242.84|10
165.231.0.242|10
171.25.193.131|10
197.231.221.211|10
109.163.234.7|10
80.82.65.21|10
185.170.42.4|10
212.21.66.6|10
62.102.148.67|10
71.6.146.185|10
192.160.102.164|10
199.87.154.255|10
37.123.133.148|10
163.172.67.180|10
192.42.116.16|10
51.15.53.83|9
185.117.215.9|9
80.82.77.139|9
87.118.126.150|9
209.222.77.220|9
61.177.21.226|9
109.163.234.9|9
115.159.241.197|9
216.218.222.12|9
122.97.218.114|9
171.25.193.78|9
111.40.166.130|9
91.197.232.108|9
185.129.62.63|9
89.248.168.30|9
166.70.207.2|9
176.126.252.11|9
77.247.181.165|9
77.247.181.163|9
185.170.41.8|8
193.90.12.86|8
94.23.173.249|8
198.20.69.98|8
91.197.232.109|8
91.197.232.107|8
128.52.128.105|8
171.25.193.132|8
92.222.84.136|8
58.48.178.200|8
61.155.238.89|8
119.78.254.4|8
65.19.167.130|8
94.102.49.190|8
195.154.217.29|8
109.163.234.8|8
183.111.108.56|8
114.255.78.180|8
64.113.32.29|8
113.209.68.135|8
71.6.146.186|8
176.10.104.243|8
176.10.104.240|8
182.118.11.35|8
82.221.105.6|8
176.126.252.12|8
178.20.55.18|8
94.102.49.193|8
111.40.168.90|8
71.6.158.166|8
51.15.40.233|8
221.122.101.203|8
192.160.102.166|8
111.11.27.140|8
125.39.58.14|8
116.228.236.206|8
62.210.105.116|8
51.255.202.66|8
119.249.54.93|8
85.248.227.163|8
