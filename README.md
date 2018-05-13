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

Wall of shame (2018-05-13)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
59.63.43.173|-|9
80.82.77.139|dojo.census.shodan.io|9
5.188.10.185|-|9
210.13.64.18|-|8
82.221.105.6|census10.shodan.io|8
219.147.91.14|14.91.147.219.broad.dq.hl.dynamic.163data.com.cn|8
60.173.82.156|-|8
61.153.56.30|-|8
45.55.33.185|-|8
66.206.39.85|66-206-39-85.static.as40244.net|8
178.62.250.237|-|8
119.29.80.17|-|8
37.193.120.203|l37-193-120-203.novotelecom.ru|8
218.241.161.50|-|8
112.73.74.104|ns2.eflydns.net|8
222.124.18.155|opted-out-dns2.telkom.net.id|8
