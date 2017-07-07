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

Wall of shame (2017-07-07)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|10
171.25.193.131|tor-exit7-readme.dfri.se|9
207.244.70.35|-|9
163.172.136.101|tor.ohundred.com|9
94.242.246.24|orion.enn.lu|9
104.223.123.98|unassigned.quadranet.com|9
65.19.167.132|-|9
109.163.234.5|hessel3.torservers.net|9
64.113.32.29|tor.t-3.net|9
171.25.193.77|tor-exit1-readme.dfri.se|9
171.25.193.78|tor-exit4-readme.dfri.se|9
80.82.77.139|dojo.census.shodan.io|9
176.10.104.240|tor1e1.digitale-gesellschaft.ch|9
212.21.66.6|tor-exit-4.all.de|9
176.126.252.11|chulak.enn.lu|9
198.96.155.3|exit.tor.uwaterloo.ca|9
193.15.16.4|-|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
166.70.207.2|this.is.a.tor.node.xmission.com|9
193.90.12.89|freebogatov-4.multisec.no|9
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|9
80.82.77.33|sky.census.shodan.io|8
94.142.242.84|tor-exit-1.zenger.nl|8
171.25.193.132|tor-exit6-readme.dfri.se|8
46.165.223.217|tor-elpresidente.piraten-nds.de|8
65.19.167.130|-|8
65.19.167.131|-|8
109.163.234.7|edwardsnowden0.torservers.net|8
109.163.234.2|hessel0.torservers.net|8
72.2.170.24|-|8
199.249.223.63|-|8
94.242.246.23|destiny.enn.lu|8
91.213.8.236|torsrvs.snydernet.net|8
111.40.166.130|-|8
199.87.154.255|tor.les.net|8
176.10.104.243|tor2e1.digitale-gesellschaft.ch|8
121.14.7.244|-|8
62.102.148.67|-|8
71.6.146.185|pirate.census.shodan.io|8
176.126.252.12|aurora.enn.lu|8
89.248.167.131|mason.census.shodan.io|8
222.47.26.140|-|8
162.247.72.7|korematsu.tor-exit.calyxinstitute.org|8
222.47.26.139|-|8
149.56.223.241|exit0.liskov.tor-relays.net|8
77.247.181.163|lumumba.torservers.net|8
163.172.67.180|tor-exit-readme.memcpy.io|8
193.90.12.87|freebogatov-2.multisec.no|8
185.38.14.171|tor-exit.r2.apx.pub|8
37.220.35.202|tor-exit.r3.apx.pub|8
193.70.95.180|ip180.ip-193-70-95.eu|8
