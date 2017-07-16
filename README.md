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

Wall of shame (2017-07-16)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|11
64.113.32.29|tor.t-3.net|10
171.25.193.77|tor-exit1-readme.dfri.se|10
171.25.193.78|tor-exit4-readme.dfri.se|10
199.87.154.255|tor.les.net|10
176.10.104.240|tor1e1.digitale-gesellschaft.ch|10
71.6.146.185|pirate.census.shodan.io|10
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|10
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|10
171.25.193.131|tor-exit7-readme.dfri.se|9
171.25.193.132|tor-exit6-readme.dfri.se|9
207.244.70.35|-|9
80.82.77.139|dojo.census.shodan.io|9
163.172.136.101|tor.ohundred.com|9
171.25.193.25|tor-exit5-readme.dfri.se|9
197.231.221.211|exit1.ipredator.se|9
94.242.246.24|orion.enn.lu|9
212.21.66.6|tor-exit-4.all.de|9
62.210.37.82|62-210-37-82.rev.poneytelecom.eu|9
198.96.155.3|exit.tor.uwaterloo.ca|9
193.15.16.4|-|9
163.172.67.180|tor-exit-readme.memcpy.io|9
51.255.202.66|tor.asmer.pro|9
51.15.53.83|83-53-15-51.rev.cloud.scaleway.com|8
94.142.242.84|tor-exit-1.zenger.nl|8
199.249.223.71|-|8
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|8
198.245.60.8|ns529549.ip-198-245-60.net|8
128.52.128.105|tor-exit.csail.mit.edu|8
204.11.50.131|tor-exit.boingboing.net|8
46.165.223.217|tor-elpresidente.piraten-nds.de|8
164.132.51.91|91.ip-164-132-51.eu|8
217.115.10.131|tor1.anonymizer.ccc.de|8
92.222.84.136|136.ip-92-222-84.eu|8
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|8
97.74.237.196|ip-97-74-237-196.ip.secureserver.net|8
104.223.123.98|unassigned.quadranet.com|8
155.4.230.97|h-4-230-97.A328.priv.bahnhof.se|8
65.19.167.132|-|8
162.247.72.27|turing.tor-exit.calyxinstitute.org|8
176.126.252.11|chulak.enn.lu|8
109.163.234.7|edwardsnowden0.torservers.net|8
187.18.118.155|r247-pw-matorico.ibys.com.br|8
212.129.18.55|212-129-18-55.rev.poneytelecom.eu|8
5.196.1.129|tor.thd.ninja|8
80.67.172.162|algrothendieck.globenet.org|8
130.226.169.137|-|8
193.70.95.180|ip180.ip-193-70-95.eu|8
94.242.246.23|destiny.enn.lu|8
89.248.172.16|house.census.shodan.io|8
149.56.223.241|exit0.liskov.tor-relays.net|8
162.213.3.221|tor-exit1.sjc02.svwh.net|8
193.171.202.150|-|8
5.254.112.154|lh31138.voxility.net|8
176.10.104.243|tor2e1.digitale-gesellschaft.ch|8
95.128.43.164|exit-1.fr.tor.aquaray.com|8
62.102.148.67|-|8
89.248.167.131|mason.census.shodan.io|8
185.129.62.62|tor01.zencurity.dk|8
64.211.24.227|-|8
192.160.102.166|chaucer.relay.coldhak.com|8
178.17.170.196|178-17-170-196.ip.as43289.net|8
192.160.102.170|ogopogo.relay.coldhak.com|8
166.70.207.2|this.is.a.tor.node.xmission.com|8
5.254.79.66|lh31139.voxility.net|8
193.90.12.87|freebogatov-2.multisec.no|8
193.90.12.86|freebogatov-1.multisec.no|8
193.90.12.89|freebogatov-4.multisec.no|8
72.52.75.27|-|8
66.70.217.179|tor.cusse.org|8
51.15.10.158|51-15-10-158.powervps.ru|8
176.126.252.12|aurora.enn.lu|8
213.61.149.100|-|8
193.90.12.90|freebogatov-5.multisec.no|8
37.187.129.166|ns316491.ip-37-187-129.eu|8
85.248.227.165|-|8
85.248.227.163|ori.enn.lu|8
