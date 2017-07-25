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

Wall of shame (2017-07-25)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
51.255.202.66|tor.asmer.pro|11
130.226.169.137|-|10
171.25.193.78|tor-exit4-readme.dfri.se|10
193.15.16.4|-|10
199.87.154.255|tor.les.net|10
176.10.104.243|tor2e1.digitale-gesellschaft.ch|10
94.142.242.84|tor-exit-1.zenger.nl|9
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|9
89.234.157.254|marylou.nos-oignons.net|9
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|9
197.231.221.211|exit1.ipredator.se|9
65.19.167.131|-|9
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|9
77.109.139.87|-|9
80.67.172.162|algrothendieck.globenet.org|9
146.185.177.103|tor-exit.ohdoom.net|9
94.242.246.24|orion.enn.lu|9
212.129.18.55|212-129-18-55.rev.poneytelecom.eu|9
171.25.193.77|tor-exit1-readme.dfri.se|9
51.15.52.230|230-52-15-51.rev.cloud.scaleway.com|9
176.10.104.240|tor1e1.digitale-gesellschaft.ch|9
216.239.90.19|tor-gateway.vif.com|9
80.82.77.139|dojo.census.shodan.io|9
95.128.43.164|exit-1.fr.tor.aquaray.com|9
71.6.146.185|pirate.census.shodan.io|9
198.96.155.3|exit.tor.uwaterloo.ca|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
79.137.67.116|ns3067031.ip-79-137-67.eu|9
204.85.191.30|tor00.telenet.unc.edu|9
213.61.149.100|-|9
37.187.129.166|ns316491.ip-37-187-129.eu|9
80.82.77.33|sky.census.shodan.io|8
62.210.129.246|relay1.tor.openinternet.io|8
171.25.193.131|tor-exit7-readme.dfri.se|8
171.25.193.132|tor-exit6-readme.dfri.se|8
81.30.144.118|srv1306.fastwebserver.de|8
164.132.51.91|91.ip-164-132-51.eu|8
78.109.23.1|tornode.torreactor.ml|8
162.247.72.201|kunstler.tor-exit.calyxinstitute.org|8
171.25.193.20|tor-exit0-readme.dfri.se|8
171.25.193.25|tor-exit5-readme.dfri.se|8
104.223.123.98|unassigned.quadranet.com|8
193.171.202.150|-|8
91.223.82.156|hosted-by.iws.co|8
5.196.1.129|tor.thd.ninja|8
178.17.174.14|178-17-174-14.ip.as43289.net|8
185.170.42.4|-|8
212.21.66.6|tor-exit-4.all.de|8
198.20.70.114|census3.shodan.io|8
62.102.148.67|-|8
5.199.130.188|tor.piratenpartei-nrw.de|8
79.172.193.32|toreador.webenlet.hu|8
89.248.172.16|house.census.shodan.io|8
176.126.252.12|aurora.enn.lu|8
178.20.55.16|marcuse-1.nos-oignons.net|8
89.248.167.131|mason.census.shodan.io|8
62.210.37.82|62-210-37-82.rev.poneytelecom.eu|8
51.15.40.233|cheeki-breeki.oignon.ovh|8
162.247.72.199|jaffer.tor-exit.calyxinstitute.org|8
64.211.24.227|-|8
219.146.120.74|-|8
59.41.103.97|-|8
149.56.223.241|exit0.liskov.tor-relays.net|8
163.172.67.180|tor-exit-readme.memcpy.io|8
193.90.12.87|freebogatov-2.multisec.no|8
193.90.12.86|freebogatov-1.multisec.no|8
193.90.12.89|freebogatov-4.multisec.no|8
185.38.14.171|tor-exit.r2.apx.pub|8
37.220.35.202|tor-exit.r3.apx.pub|8
79.134.234.247|sunfire-cape.gate.wayne-enterprises.company|8
51.15.63.229|229-63-15-51.rev.cloud.scaleway.com|8
85.248.227.163|ori.enn.lu|8
