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

Wall of shame (2017-07-10)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|9
212.21.66.6|tor-exit-4.all.de|9
71.6.146.185|pirate.census.shodan.io|9
84.19.181.25|tor-exit2.signal.center|8
176.10.104.240|tor1e1.digitale-gesellschaft.ch|8
218.2.197.240|-|8
171.25.193.131|tor-exit7-readme.dfri.se|8
80.82.77.139|dojo.census.shodan.io|8
80.67.172.162|algrothendieck.globenet.org|8
216.218.222.12|-|8
162.213.3.221|tor-exit1.sjc02.svwh.net|8
171.25.193.77|tor-exit1-readme.dfri.se|8
171.25.193.78|tor-exit4-readme.dfri.se|8
199.87.154.255|tor.les.net|8
121.14.7.244|-|8
89.248.167.131|mason.census.shodan.io|8
222.47.26.140|-|8
192.160.102.170|ogopogo.relay.coldhak.com|8
222.47.26.139|-|8
149.56.223.241|exit0.liskov.tor-relays.net|8
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|8
166.70.207.2|this.is.a.tor.node.xmission.com|8
5.254.79.66|lh31139.voxility.net|8
66.70.217.179|tor.cusse.org|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
193.90.12.90|freebogatov-5.multisec.no|8
