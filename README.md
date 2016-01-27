![Logo](logo.png)

# IPsum [![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

**IPsum** is a Threat Intelligence Feed based on 35+ different publicly available lists of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of occurrence (for each). Greater the number, lesser the chance of false positive detection in monitored traffic. Also, to make it easier for eventual (autoban) usage, list is sorted from most (problematic) to least occurent IP addresses.

The following (black)lists are currently being utilized:
```
alienvault, autoshun, badips, bambenekconsultingc2,
botscout, bruteforceblocker, ciarmy, cruzit, cybercrimetracker,
dshieldip, emergingthreatsbot, emergingthreatscip,
malwarepatrol, maxmind, myip, nothink, openbl, openphish,
packetmailcarisirt, packetmailramnode, palevotracker, proxylists,
proxyrss, proxy, riproxies, rutgers, sblam,
securityresearch, snort, socksproxy, sslipbl, sslproxies,
torproject, torstatus, turris, voipbl, vxvault, etc.
```
