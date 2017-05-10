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

Wall of shame (2017-05-10)
----

|IP|Number of (black)lists|
|---|--:|
185.170.41.8|11
89.234.157.254|11
176.126.252.11|11
94.242.246.24|10
64.113.32.29|10
171.25.193.77|10
111.40.166.130|10
62.102.148.67|10
185.129.62.63|10
173.254.216.66|10
77.247.181.163|10
198.20.69.98|9
80.82.77.139|9
197.231.221.211|9
87.118.126.150|9
176.10.104.240|9
71.6.146.185|9
128.52.128.105|9
192.160.102.164|9
166.70.207.2|9
193.90.12.87|9
85.248.227.163|9
77.247.181.165|9
80.82.77.33|8
93.174.95.106|8
198.245.60.8|8
217.182.71.208|8
171.25.193.131|8
164.132.51.91|8
92.222.84.136|8
185.38.14.171|8
218.78.213.142|8
65.19.167.131|8
65.19.167.132|8
65.19.167.134|8
193.171.202.150|8
94.102.49.190|8
109.163.234.5|8
109.163.234.7|8
195.154.251.209|8
77.109.139.87|8
185.170.42.4|8
216.218.222.11|8
176.10.104.243|8
216.239.90.19|8
178.217.187.39|8
71.6.146.186|8
176.126.252.12|8
192.42.116.16|8
163.172.67.180|8
217.20.113.18|8
62.210.105.116|8
51.255.202.66|8
37.187.129.166|8
137.74.167.96|8
199.249.223.72|8
85.248.227.164|8
