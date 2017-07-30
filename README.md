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

Wall of shame (2017-07-30)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
79.137.67.116|ns3067031.ip-79-137-67.eu|10
171.25.193.25|tor-exit5-readme.dfri.se|10
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|10
171.25.193.78|tor-exit4-readme.dfri.se|10
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|10
199.87.154.255|tor.les.net|10
176.10.104.243|tor2e1.digitale-gesellschaft.ch|9
78.109.23.1|tornode.torreactor.ml|9
197.231.221.211|exit1.ipredator.se|9
193.15.16.4|-|9
66.70.217.179|tor.cusse.org|9
80.82.77.33|sky.census.shodan.io|8
193.90.12.87|tor-2.multisec.no|8
171.25.193.131|tor-exit7-readme.dfri.se|8
89.234.157.254|marylou.nos-oignons.net|8
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|8
171.25.193.20|tor-exit0-readme.dfri.se|8
176.10.104.240|tor1e1.digitale-gesellschaft.ch|8
65.19.167.132|-|8
77.109.139.87|-|8
80.67.172.162|algrothendieck.globenet.org|8
130.226.169.137|-|8
171.25.193.77|tor-exit1-readme.dfri.se|8
51.15.52.230|230-52-15-51.rev.cloud.scaleway.com|8
80.82.77.139|dojo.census.shodan.io|8
175.6.27.205|-|8
62.102.148.67|-|8
121.14.7.244|-|8
185.113.128.234|nexuscheetah.com|8
89.144.12.15|-|8
192.160.102.170|ogopogo.relay.coldhak.com|8
222.186.61.176|-|8
93.174.90.30|2.shulgin.nl.torexit.haema.co.uk|8
193.90.12.86|tor-1.multisec.no|8
51.255.202.66|tor.asmer.pro|8
37.187.129.166|ns316491.ip-37-187-129.eu|8
118.233.251.86|118-233-251-86.dynamic.kbronet.com.tw|8
199.249.223.72|-|8
216.218.222.12|-|8
36.155.7.4|-|8
163.172.67.180|tor-exit-readme.memcpy.io|8
