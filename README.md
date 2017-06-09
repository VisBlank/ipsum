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

Wall of shame (2017-06-09)
----

|IP|Number of (black)lists|
|---|--:|
89.234.157.254|11
178.217.187.39|10
62.210.105.116|10
171.25.193.131|9
155.4.230.97|9
171.25.193.77|9
199.87.154.255|9
94.142.242.84|8
218.2.197.240|8
78.109.23.1|8
81.171.2.145|8
163.172.136.101|8
94.242.246.24|8
171.25.193.25|8
176.126.252.11|8
166.70.207.2|8
51.255.202.66|8
212.129.58.61|8
171.25.193.78|8
111.40.166.130|8
193.15.16.4|8
193.70.95.180|8
212.21.66.6|8
71.6.146.185|8
62.210.37.82|8
85.248.227.165|8
72.51.37.205|8
192.42.116.16|8
193.90.12.87|8
193.90.12.86|8
85.248.227.164|8
207.244.70.35|8
