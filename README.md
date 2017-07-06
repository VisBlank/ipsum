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

Wall of shame (2017-07-06)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|11
171.25.193.131|tor-exit7-readme.dfri.se|10
176.10.104.240|tor1e1.digitale-gesellschaft.ch|10
71.6.146.185|pirate.census.shodan.io|10
80.82.77.33|sky.census.shodan.io|9
94.102.49.190|flower.census.shodan.io|9
109.163.234.5|hessel3.torservers.net|9
199.87.154.255|tor.les.net|9
193.15.16.4|-|9
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|9
94.142.242.84|tor-exit-1.zenger.nl|8
218.2.197.240|-|8
171.25.193.132|tor-exit6-readme.dfri.se|8
207.244.70.35|-|8
180.164.38.174|-|8
66.240.236.119|census6.shodan.io|8
163.172.136.101|tor.ohundred.com|8
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|8
94.242.246.24|orion.enn.lu|8
64.113.32.29|tor.t-3.net|8
94.242.246.23|destiny.enn.lu|8
171.25.193.77|tor-exit1-readme.dfri.se|8
171.25.193.78|tor-exit4-readme.dfri.se|8
111.40.166.130|-|8
80.82.77.139|dojo.census.shodan.io|8
212.21.66.6|tor-exit-4.all.de|8
198.20.70.114|census3.shodan.io|8
62.102.148.67|-|8
176.126.252.11|chulak.enn.lu|8
62.210.37.82|62-210-37-82.rev.poneytelecom.eu|8
222.47.26.140|-|8
222.47.26.139|-|8
198.96.155.3|exit.tor.uwaterloo.ca|8
77.247.181.163|lumumba.torservers.net|8
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|8
166.70.207.2|this.is.a.tor.node.xmission.com|8
193.90.12.89|freebogatov-4.multisec.no|8
162.247.73.206|rosaluxemburg.tor-exit.calyxinstitute.org|8
