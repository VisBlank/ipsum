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

Wall of shame (2017-08-02)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
171.25.193.77|tor-exit1-readme.dfri.se|11
176.10.104.243|tor2e1.digitale-gesellschaft.ch|11
171.25.193.25|tor-exit5-readme.dfri.se|10
193.90.12.87|tor-2.multisec.no|10
51.15.53.83|83-53-15-51.rev.cloud.scaleway.com|9
78.109.23.1|tornode.torreactor.ml|9
162.247.72.202|djb.tor-exit.calyxinstitute.org|9
197.231.221.211|exit1.ipredator.se|9
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|9
94.102.49.190|flower.census.shodan.io|9
80.67.172.162|algrothendieck.globenet.org|9
130.226.169.137|-|9
146.185.177.103|tor-exit.ohdoom.net|9
171.25.193.78|tor-exit4-readme.dfri.se|9
199.87.154.255|tor.les.net|9
216.218.222.11|-|9
51.15.52.230|230-52-15-51.rev.cloud.scaleway.com|9
176.10.104.240|tor1e1.digitale-gesellschaft.ch|9
71.6.146.185|pirate.census.shodan.io|9
185.113.128.234|nexuscheetah.com|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
79.137.67.116|ns3067031.ip-79-137-67.eu|9
166.70.207.2|this.is.a.tor.node.xmission.com|9
193.90.12.86|tor-1.multisec.no|9
213.61.149.100|-|9
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|9
94.142.242.84|tor-exit-1.zenger.nl|8
218.2.197.240|-|8
128.52.128.105|tor-exit.csail.mit.edu|8
171.25.193.131|tor-exit7-readme.dfri.se|8
171.25.193.132|tor-exit6-readme.dfri.se|8
207.244.70.35|-|8
163.172.151.250|250-151-172-163.rev.cloud.scaleway.com|8
46.165.223.217|tor-elpresidente.piraten-nds.de|8
89.234.157.254|marylou.nos-oignons.net|8
163.172.136.101|tor.ohundred.com|8
171.25.193.20|tor-exit0-readme.dfri.se|8
162.247.72.217|perry.fellwock.tor-exit.calyxinstitute.org|8
65.19.167.132|-|8
176.126.252.11|chulak.enn.lu|8
77.109.139.87|-|8
64.113.32.29|tor.t-3.net|8
94.242.246.23|destiny.enn.lu|8
94.242.246.24|orion.enn.lu|8
212.129.18.55|212-129-18-55.rev.poneytelecom.eu|8
89.31.57.5|dreamatorium.badexample.net|8
163.172.137.174|174-137-172-163.rev.cloud.scaleway.com|8
185.170.42.4|-|8
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|8
216.239.90.19|tor-gateway.vif.com|8
212.21.66.6|tor-exit-4.all.de|8
198.20.70.114|census3.shodan.io|8
80.82.77.139|dojo.census.shodan.io|8
191.96.249.97|-|8
71.6.146.186|inspire.census.shodan.io|8
176.126.252.12|aurora.enn.lu|8
178.20.55.16|marcuse-1.nos-oignons.net|8
170.250.140.52|170.250.140.52.hwccustomers.com|8
41.206.188.206|-|8
62.210.37.82|62-210-37-82.rev.poneytelecom.eu|8
89.144.12.15|-|8
192.160.102.166|chaucer.relay.coldhak.com|8
185.29.8.132|ip-8-132.dataclub.biz|8
64.124.32.84|64.124.32.84.IPYX-102914-ZYO.zip.zayo.com|8
149.56.223.241|exit0.liskov.tor-relays.net|8
198.96.155.3|exit.tor.uwaterloo.ca|8
93.174.90.30|2.shulgin.nl.torexit.haema.co.uk|8
193.15.16.4|-|8
193.90.12.89|tor-4.multisec.no|8
66.70.217.179|tor.cusse.org|8
51.255.202.66|tor.asmer.pro|8
37.187.129.166|ns316491.ip-37-187-129.eu|8
162.247.73.206|rosaluxemburg.tor-exit.calyxinstitute.org|8
5.196.1.129|tor.thd.ninja|8
