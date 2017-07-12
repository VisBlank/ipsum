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

Wall of shame (2017-07-12)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
171.25.193.78|tor-exit4-readme.dfri.se|11
176.10.104.240|tor1e1.digitale-gesellschaft.ch|11
89.234.157.254|marylou.nos-oignons.net|10
65.19.167.132|-|10
171.25.193.77|tor-exit1-readme.dfri.se|10
199.87.154.255|tor.les.net|10
212.21.66.6|tor-exit-4.all.de|10
71.6.146.185|pirate.census.shodan.io|10
62.210.37.82|62-210-37-82.rev.poneytelecom.eu|10
193.90.12.86|freebogatov-1.multisec.no|10
85.248.227.165|-|10
171.25.193.131|tor-exit7-readme.dfri.se|9
207.244.70.35|-|9
171.25.193.25|tor-exit5-readme.dfri.se|9
104.223.123.98|unassigned.quadranet.com|9
82.221.105.6|census10.shodan.io|9
64.113.32.29|tor.t-3.net|9
94.242.246.23|destiny.enn.lu|9
95.128.43.164|exit-1.fr.tor.aquaray.com|9
62.102.148.67|-|9
77.247.181.163|lumumba.torservers.net|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
163.172.67.180|tor-exit-readme.memcpy.io|9
5.254.79.66|lh31139.voxility.net|9
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|9
51.255.202.66|tor.asmer.pro|9
213.61.149.100|-|9
162.247.73.206|rosaluxemburg.tor-exit.calyxinstitute.org|9
80.82.77.33|sky.census.shodan.io|8
94.142.242.84|tor-exit-1.zenger.nl|8
199.249.223.71|-|8
62.210.115.87|62-210-115-87.rev.poneytelecom.eu|8
146.185.177.103|tor-exit.ohdoom.net|8
198.245.60.8|ns529549.ip-198-245-60.net|8
171.25.193.132|tor-exit6-readme.dfri.se|8
163.172.151.250|250-151-172-163.rev.cloud.scaleway.com|8
80.82.77.139|dojo.census.shodan.io|8
164.132.51.91|91.ip-164-132-51.eu|8
163.172.136.101|tor.ohundred.com|8
163.172.212.115|163-172-212-115.rev.poneytelecom.eu|8
97.74.237.196|ip-97-74-237-196.ip.secureserver.net|8
197.231.221.211|exit1.ipredator.se|8
82.221.105.7|census11.shodan.io|8
80.67.172.162|algrothendieck.globenet.org|8
109.163.234.4|hessel2.torservers.net|8
109.163.234.7|edwardsnowden0.torservers.net|8
216.218.134.12|-|8
171.25.193.20|tor-exit0-readme.dfri.se|8
5.196.1.129|tor.thd.ninja|8
216.218.222.12|-|8
94.242.246.24|orion.enn.lu|8
91.213.8.236|torsrvs.snydernet.net|8
212.129.18.55|212-129-18-55.rev.poneytelecom.eu|8
193.15.16.4|-|8
51.15.52.230|230-52-15-51.rev.cloud.scaleway.com|8
176.10.104.243|tor2e1.digitale-gesellschaft.ch|8
216.239.90.19|tor-gateway.vif.com|8
198.20.70.114|census3.shodan.io|8
5.199.130.188|tor.piratenpartei-nrw.de|8
83.223.0.219|-|8
89.248.172.16|house.census.shodan.io|8
176.126.252.12|aurora.enn.lu|8
176.126.252.11|chulak.enn.lu|8
178.20.55.16|marcuse-1.nos-oignons.net|8
170.250.140.52|170.250.140.52.hwccustomers.com|8
37.187.129.166|ns316491.ip-37-187-129.eu|8
89.248.167.131|mason.census.shodan.io|8
51.15.40.233|cheeki-breeki.oignon.ovh|8
185.129.62.62|tor01.zencurity.dk|8
162.247.72.199|jaffer.tor-exit.calyxinstitute.org|8
64.211.24.227|-|8
192.160.102.164|snowfall.relay.coldhak.com|8
192.160.102.170|ogopogo.relay.coldhak.com|8
62.212.73.141|-|8
93.174.90.30|2.shulgin.nl.torexit.haema.co.uk|8
77.247.181.165|politkovskaja.torservers.net|8
111.40.166.130|-|8
193.90.12.87|freebogatov-2.multisec.no|8
193.90.12.89|freebogatov-4.multisec.no|8
72.52.75.27|-|8
66.70.217.179|tor.cusse.org|8
51.15.10.158|51-15-10-158.powervps.ru|8
193.90.12.90|freebogatov-5.multisec.no|8
85.248.227.163|ori.enn.lu|8
185.100.87.210|-|8
