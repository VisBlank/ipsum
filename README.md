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

Wall of shame (2017-02-17)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|10
171.25.193.77|10
197.231.221.211|9
176.126.252.12|9
176.10.104.243|9
221.194.44.219|9
185.110.132.202|9
119.249.54.71|8
222.209.224.80|8
110.167.224.182|8
171.25.193.131|8
200.93.235.115|8
93.115.95.216|8
192.36.27.4|8
191.96.249.48|8
37.220.35.202|8
221.194.47.208|8
218.83.155.86|8
115.135.8.237|8
193.201.224.210|8
221.229.162.98|8
171.25.193.78|8
218.2.108.2|8
117.18.79.201|8
178.217.187.39|8
121.18.238.109|8
193.201.224.39|8
195.3.144.213|8
123.31.32.68|8
121.18.238.114|8
149.56.229.16|8
60.205.210.125|8
217.52.242.154|8
178.20.157.206|8
113.124.138.2|8
93.103.179.52|8
163.172.67.180|8
37.187.129.166|8
77.247.181.165|8
181.57.149.131|8
