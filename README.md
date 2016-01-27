![Logo](logo.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

**IPsum** is a threat intelligence feed based on 30+ different publicly available lists of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of occurrence (for each). Greater the number, lesser the chance of false positive detection in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh conservative and ready-to-deploy auto-ban list of "bad IPs" that appear on more than 4 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "[1-4]$" | cut -f 1
```

Fresh list can be found [here](https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt).
