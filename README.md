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

Wall of shame (2017-01-28)
----

|IP|Number of (black)lists|
|---|--:|
171.25.193.77|10
89.234.157.254|9
197.231.221.211|9
65.19.167.132|9
218.2.0.16|8
60.11.118.110|8
128.52.128.105|8
203.162.37.206|8
209.222.77.220|8
109.163.234.7|8
191.96.249.48|8
60.2.127.118|8
46.166.148.176|8
162.209.99.126|8
171.25.193.78|8
216.239.90.19|8
178.217.187.39|8
218.3.140.74|8
151.80.42.102|8
51.15.40.233|8
144.12.78.162|8
37.49.224.115|8
179.233.94.73|8
166.70.207.2|8
186.46.85.2|8
115.85.192.40|8
185.56.82.66|8
85.248.227.163|8
91.224.160.108|8
77.247.181.165|8
93.103.179.52|8
