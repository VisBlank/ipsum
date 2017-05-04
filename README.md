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

Wall of shame (2017-05-04)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
171.25.193.77|11
109.163.234.5|10
185.170.42.4|10
62.102.148.67|10
192.160.102.164|10
173.254.216.66|10
193.90.12.86|9
198.20.69.98|9
171.25.193.131|9
197.231.221.211|9
163.172.67.180|9
171.25.193.78|9
212.21.66.6|9
71.6.146.185|9
128.52.128.105|9
89.248.168.30|9
77.247.181.163|9
176.126.252.11|9
94.242.246.24|9
185.170.41.8|8
198.245.60.8|8
80.82.77.139|8
87.118.126.150|8
209.222.77.220|8
82.221.105.7|8
176.126.252.12|8
109.163.234.8|8
109.163.234.9|8
64.113.32.29|8
77.109.139.87|8
193.15.16.4|8
221.207.236.189|8
193.70.95.180|8
176.10.104.243|8
176.10.104.240|8
71.6.146.186|8
183.134.110.184|8
193.227.49.83|8
51.15.40.233|8
199.87.154.255|8
217.20.113.19|8
62.210.105.116|8
51.255.202.66|8
