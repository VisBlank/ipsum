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

Wall of shame (2017-07-05)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
176.10.104.240|tor1e1.digitale-gesellschaft.ch|9
104.223.123.98|unassigned.quadranet.com|9
80.82.77.33|sky.census.shodan.io|8
218.2.197.240|-|8
171.25.193.131|tor-exit7-readme.dfri.se|8
89.234.157.254|marylou.nos-oignons.net|8
92.222.84.136|136.ip-92-222-84.eu|8
115.231.218.24|-|8
171.25.193.77|tor-exit1-readme.dfri.se|8
111.40.166.130|-|8
199.87.154.255|tor.les.net|8
18.85.22.204|wholesomeserver.media.mit.edu|8
80.82.77.139|dojo.census.shodan.io|8
71.6.146.185|pirate.census.shodan.io|8
163.172.73.217|163-172-73-217.rev.poneytelecom.eu|8
222.47.26.139|-|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
79.124.59.202|-|8
