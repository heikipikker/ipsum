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

Wall of shame (2018-04-10)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
197.231.221.211|exit1.ipredator.se|10
5.188.10.179|-|10
171.25.193.78|tor-exit4-readme.dfri.se|9
221.194.44.211|-|9
106.3.40.136|undefine.inidc.com.cn|9
212.21.66.6|tor-exit-4.all.de|8
218.156.85.17|-|8
122.226.181.166|-|8
46.148.20.25|druid.vps|8
221.194.47.243|-|8
171.25.193.25|tor-exit5-readme.dfri.se|8
104.223.123.98|unassigned.quadranet.com|8
218.9.25.103|-|8
60.173.82.156|-|8
5.101.40.81|-|8
221.194.47.236|-|8
221.194.47.239|-|8
222.174.255.14|-|8
91.205.173.66|vmi169006.contaboserver.net|8
193.15.16.4|-|8
80.82.77.139|dojo.census.shodan.io|8
89.248.167.131|mason.census.shodan.io|8
202.97.205.78|-|8
185.244.25.189|-|8
117.156.15.251|-|8
219.147.91.14|14.91.147.219.broad.dq.hl.dynamic.163data.com.cn|8
31.220.42.231|-|8
115.238.245.8|-|8
115.238.245.6|-|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
150.249.92.178|fp96f95cb2.tkyc216.ap.nuro.jp|8
58.218.213.253|-|8
