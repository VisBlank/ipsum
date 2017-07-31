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

Wall of shame (2017-07-31)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
197.231.221.211|exit1.ipredator.se|11
193.90.12.86|tor-1.multisec.no|11
79.137.67.116|ns3067031.ip-79-137-67.eu|10
171.25.193.77|tor-exit1-readme.dfri.se|10
71.6.146.185|pirate.census.shodan.io|10
171.25.193.131|tor-exit7-readme.dfri.se|9
171.25.193.132|tor-exit6-readme.dfri.se|9
46.165.223.217|tor-elpresidente.piraten-nds.de|9
171.25.193.25|tor-exit5-readme.dfri.se|9
77.109.139.87|-|9
171.25.193.78|tor-exit4-readme.dfri.se|9
199.87.154.255|tor.les.net|9
176.10.104.243|tor2e1.digitale-gesellschaft.ch|9
176.10.104.240|tor1e1.digitale-gesellschaft.ch|9
216.239.90.19|tor-gateway.vif.com|9
212.21.66.6|tor-exit-4.all.de|9
198.20.70.114|census3.shodan.io|9
149.56.223.241|exit0.liskov.tor-relays.net|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
166.70.207.2|this.is.a.tor.node.xmission.com|9
193.90.12.87|tor-2.multisec.no|9
213.61.149.100|-|9
37.187.129.166|ns316491.ip-37-187-129.eu|9
94.142.242.84|tor-exit-1.zenger.nl|8
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|8
185.165.168.186|-|8
128.52.128.105|tor-exit.csail.mit.edu|8
204.11.50.131|tor-exit.boingboing.net|8
163.172.151.250|250-151-172-163.rev.cloud.scaleway.com|8
89.234.157.254|marylou.nos-oignons.net|8
78.109.23.1|tornode.torreactor.ml|8
162.247.72.201|kunstler.tor-exit.calyxinstitute.org|8
162.247.72.200|kiriakou.tor-exit.calyxinstitute.org|8
94.242.246.23|destiny.enn.lu|8
171.25.193.20|tor-exit0-readme.dfri.se|8
193.171.202.150|-|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
104.200.20.46|tor-exit.bynumlaw.net|8
80.67.172.162|algrothendieck.globenet.org|8
185.100.84.82|-|8
130.226.169.137|-|8
146.185.177.103|tor-exit.ohdoom.net|8
64.113.32.29|tor.t-3.net|8
94.242.246.24|orion.enn.lu|8
204.8.156.142|cs-tor.bu.edu|8
79.134.234.247|sunfire-cape.gate.wayne-enterprises.company|8
198.96.155.3|exit.tor.uwaterloo.ca|8
51.15.52.230|230-52-15-51.rev.cloud.scaleway.com|8
80.82.77.139|dojo.census.shodan.io|8
95.128.43.164|exit-1.fr.tor.aquaray.com|8
62.102.148.67|-|8
71.6.146.186|inspire.census.shodan.io|8
178.20.55.18|marcuse-2.nos-oignons.net|8
178.20.55.16|marcuse-1.nos-oignons.net|8
89.144.12.15|-|8
162.247.72.7|korematsu.tor-exit.calyxinstitute.org|8
93.174.90.30|2.shulgin.nl.torexit.haema.co.uk|8
193.15.16.4|-|8
66.70.217.179|tor.cusse.org|8
176.126.252.12|aurora.enn.lu|8
204.85.191.30|tor00.telenet.unc.edu|8
51.255.202.66|tor.asmer.pro|8
36.155.7.4|-|8
